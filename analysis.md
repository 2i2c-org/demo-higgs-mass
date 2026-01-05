---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.18.1
kernelspec:
  name: python3
  display_name: Python 3 (ipykernel)
  language: python
---

# Finding the Higgs Boson

```{code-cell} ipython3
import awkward as ak
import numpy as np
import hist
import particle
import hepunits
import vector
vector.register_awkward()
```

Load some data

```{code-cell} ipython3
raw_events = ak.from_parquet("data/SMHiggsToZZTo4L.parquet")

raw_events.type.show()
```

Let's restructure this to take advantage of structural operations.

```{code-cell} ipython3
def make_record_from_prefix(arr, prefix, name):
    prefix_with_separator = f"{prefix}_"
    arr_items = ak.unzip(arr, how=dict).items()
    structure = {
       n.removeprefix(prefix_with_separator): v for n, v in arr_items
       if n.startswith(prefix_with_separator)
    }
    return ak.zip(structure, with_name=name)

events = ak.zip({
    "muons": make_record_from_prefix(raw_events, "Muon", "Momentum4D"),
    "electrons": make_record_from_prefix(raw_events, "Electron", "Momentum4D"),
}, depth_limit=1)

events.type.show()
```

## H → ZZ → 4μ or 4e

+++

Find events consisting of four same-flavour leptons

```{code-cell} ipython3
four_muons = ak.combinations(events.muons, 4)
four_electrons = ak.combinations(events.electrons, 4)
```

Compute the invariant mass of the frame
$$
M_0^2 = \left(\sum_i E_i\right)^{2}-\left\|\sum_i \mathbf {p}_i\right\|^{2}
$$
by adding together all of the four-momentum vectors 
$$
p=\left(p^{0},p^{1},p^{2},p^{3}\right)=\left({\frac {E}{c}},p_{x},p_{y},p_{z}\right).
$$

```{code-cell} ipython3
four_muons_mass = (four_muons['0'] + four_muons['1'] + four_muons['2'] + four_muons['3']).mass
four_electrons_mass = (four_electrons['0'] + four_electrons['1'] + four_electrons['2'] + four_electrons['3']).mass
```

Histogram the result

```{code-cell} ipython3
(
    hist.Hist.new.Reg(128, 0, 150, label="Mass /$\\text{GeV}\\,c^{-2}$")
    .Double()
    .fill_flattened(four_muons_mass)
    .fill_flattened(four_electrons_mass)
).plot()
```

## H → ZZ → 4l

```{code-cell} ipython3
muons_plus = events.muons[events.muons.charge > 0]
muons_minus = events.muons[events.muons.charge < 0]

electrons_plus = events.electrons[events.electrons.charge > 0]
electrons_minus = events.electrons[events.electrons.charge < 0]
```

```{code-cell} ipython3
muon_plus, muon_minus, electron_plus, electron_minus = ak.unzip(
    ak.cartesian(
        (muons_plus, muons_minus, electrons_plus, electrons_minus)
    )
)
```

```{code-cell} ipython3
(
    hist.Hist.new.Reg(100, 0, 150, label="Mass /$\\text{GeV}\\,c^{-2}$")
    .Double()
    .fill_flattened((muon_plus + muon_minus + electron_plus + electron_minus).mass)
).plot()
```

```{code-cell} ipython3
ZMASS = particle.Particle.findall("Z0")[0].mass / hepunits.GeV
ZMASS
```

```{code-cell} ipython3
is_on_shell_z_muon = np.abs((muon_plus + muon_minus).mass - ZMASS) < 20
is_on_shell_z_electron = np.abs((electron_plus + electron_minus).mass - ZMASS) < 20
```

```{code-cell} ipython3
is_on_shell_z = is_on_shell_z_muon | is_on_shell_z_electron
```

```{code-cell} ipython3
(
    hist.Hist.new.Reg(100, 0, 150, label="Mass /$\\text{GeV}\\,c^{-2}$")
    .Double()
    .fill_flattened(
        (muon_plus + muon_minus + electron_plus + electron_minus).mass[is_on_shell_z]
    )
).plot();
```

```{code-cell} ipython3

```
