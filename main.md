# Discovering the Higgs Boson

## Introduction
In a conventional journey to learn about the Physical universe, most physicists are initially presented with evidence that the <wiki:photon> has particle-like properties. One of the _suprising_ facts that Physicists subsequently encounter is that photons are _massless_. Photons are one of several spin-1 <wiki:gauge_boson> particles, alongside <wiki:gluons> and <wiki:W_bosons>. [Gauge Theory](wiki:Introduction_to_gauge_theory) predicts that all gauge bosons have zero mass. Whilst this is observed to be the case for photons, we _know_ that the W boson has mass! 

:::{note}
The W boson has _greater mass than a stable isotope of Iron_!
:::

Explaining why the photon is massless and the W boson is massive was a difficult challenge in contemporary physics until the proposal of the <wiki:Higgs_mechanism>. Introduced by three different groups in 1964, the Higgs mechanism introduced a new <wiki:quantum_field> (the Higgs field) that furnishes W and Z gauge bosons with mass through interactions with the field. 

:::{pull-quote}
Prior to the invention of the Higgs mechanism, it was not known how to formulate a consistent relativistic field theory with a local symmetry which could contain both massless and massive force carriers.

-- [Brief History of the Higgs Mechanism](https://www.ph.ed.ac.uk/higgs/brief-history)
:::

In addition, the mechanism yields a massive (spin-zero) <wiki:scalar_boson> termed the Higgs boson, whose mass is derived from excitations of that field. It is this particle, through its unique decay signature, that was postulated as a candidate for experimental proof of the Higgs mechanism. In 2012, the <wiki:Higgs_boson> was discovered independently by the <wiki:Compact_Muon_Solenoid> and [ATLAS](wiki:ATLAS_experiment) experiments at the <wiki:Large_Hadron_Collider>, with a subsequent confidence of over 5 sigma — that the observed result lies more than five standard deviations (of the measurement) away from the "null hypothesis".

:::{pull-quote}
Five sigma is considered the “gold standard” in particle physics because it guarantees an extremely low likelihood of a claim being false.

-- [CERN FAQs](https://home.cern/resources/faqs/five-sigma)
:::

:::{figure} https://upload.wikimedia.org/wikipedia/commons/3/3a/Standard_deviation_diagram_micro.svg
:label: sigma-pdf

Diagram of <wiki:normal_distribution> <wiki:probability_density_function>, Ainali, CC BY-SA 3.0 <https://creativecommons.org/licenses/by-sa/3.0>, via Wikimedia Commons
:::

## Decay Modes
In the LHC, particles formed in the high energy proton-proton collisions decay almost immediately to smaller (elementary) particles. Consequently, experimentalists tend not to detect these progenitor particles, but rather observe their decay products. Through kinematic reconstruction (measuring the energy and momentum of the _entire system_ of particles), Physicists can look backwards in time to the moment of the collision itself, and learn about what took place (see @cms-event).

:::{iframe} https://cms3d.web.cern.ch/HIG-19-001-embedded/
:label: cms-event

Interactive display of an event recorded by the CMS detector in 2018, taken from https://cms.cern/news/using-golden-decay-channel-understand-production-higgs-boson.
:::

Physical particles can typically decay into a variety of different particles through a variety of different mechanisms. Each of these possible decays is known as a decay _mode_ or _channel_. One such channel for the Higgs boson is the "golden channel", whereby the Higgs boson decays into a pair of <wiki:Z_bosons>, one of which is in the ground state, which in-turn decay into two pairs of <wiki:leptons> (see @golden-channel).

:::{figure} https://higgszz.web.cern.ch/style/feynman_diagram.png
:label: golden-channel
The "golden decay channel" of the Higgs boson, taken from https://higgszz.web.cern.ch/.
:::

There are a variety of other processes that can lead to the formation of two Z bosons such that we see four leptons. These are termed "background" signals. @zz-mass shows how these separate production modes can sum together with the Higgs production channel to produce our observed signal.

:::{figure} https://cms.cern/sites/default/files/inline-images/zzmass_500.gif
:label: zz-mass
Four-lepton invariant mass distribution in the golden decay channel, taken from https://cms.cern/news/using-golden-decay-channel-understand-production-higgs-boson.
:::

## Analysis
We gain an insight into some of the analysis that was undertaken by the LHC teams by looking at simulated data. This is only a small peek into the work required — most of the difficulty in high energy physics experiments lies in the experimental capture and reconstruction of the data.

There are two kinds of channels within the golden channel that we can look out for. Either, {math}`ZZ^\star \rightarrow 4\mu` and {math}`ZZ^\star \rightarrow 4e`, or {math}`ZZ^\star \rightarrow 2\mu 2e`. In the first instance, we produce the following plots:

:::{figure} #zz-eeee-uuuu
{math}`ZZ^\star \rightarrow 4\mu` and {math}`ZZ^\star \rightarrow 4e` decay channels of the Higgs boson.
:::

But, we can also take permutations of events with 2u and 2e:


:::{figure} #zz-2u2e
{math}`ZZ^\star \rightarrow 2\mu 2e` decay channel of the Higgs boson.
:::

Through the ZZ* decay mode, we know that one of the Z bosons should be in its ground state. We can try to select events that satisfy this constraint via a "cut" that eliminates events failing this criterion:

:::{figure} #on-shell-zz-2u2e
{math}`ZZ^\star \rightarrow 2\mu 2e` decay channel of the Higgs boson gated on the ground state of Z. 

```{tip}
Click the Power button, and Play button of this figure to trigger execution.
```
:::
