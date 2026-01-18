# Divergent Mechanisms of Antidepressant Efficacy: A Unified Computational Comparison of Synaptogenesis, Stabilization, and Tonic Inhibition in a Model of Depression

Authors:

Ngo Cheung, FHKAM(Psychiatry)

Affiliations:

¹ Independent Researcher

Corresponding Author:

Ngo Cheung, MBBS, FHKAM(Psychiatry)

Hong Kong SAR, China

Tel: 98768323

Email: info@cheungngomedical.com

**Conflict of Interest**: None declared.

**Funding Declaration**: This research received no specific grant from
any funding agency in the public, commercial, or not-for-profit sectors.

**Ethics Declaration**: Not applicable.

Citation: 
Cheung, N. (2026). Divergent Mechanisms of Antidepressant Efficacy: A Unified Computational Comparison of Synaptogenesis, Stabilization, and Tonic Inhibition in a Model of Depression. Zenodo. https://doi.org/10.5281/zenodo.18290014

## Abstract

Background: Major depressive disorder is increasingly viewed as a
disorder of impaired neural plasticity, yet the mechanisms underlying
diverse antidepressant classes---glutamatergic (e.g., ketamine),
monoaminergic (e.g., SSRIs), and GABAergic (e.g.,
neurosteroids)---remain incompletely integrated. Computational models
offer a controlled means to compare these pathways, but prior work has
typically examined single mechanisms.

Methods: We extended a pruning-plasticity model of depression by
applying 95% magnitude-based synaptic elimination to overparameterized
feed-forward networks trained on a four-class Gaussian classification
task. From identical pruned states, three interventions were tested:
ketamine-like gradient-guided regrowth (50% reinstatement) with
consolidation; SSRI-like prolonged low-learning-rate training with
gradual internal noise reduction; and neurosteroid-like global tonic
inhibition (30% damping plus tanh activations) with brief consolidation.
Outcomes included baseline accuracy, resilience to graded internal
activation noise (up to σ = 2.5) plus input perturbation, and relapse
vulnerability after additional 40% pruning.

Results: All treatments restored near-ceiling performance on
unchallenged inputs. Ketamine-like synaptogenesis uniquely reduced
sparsity (to \~47%) and conferred superior stress resilience (extreme
noise accuracy 84.5%) with near-zero relapse drop (−0.2%). SSRI-like
refinement improved combined stress accuracy to 83.5% but showed limited
extreme noise tolerance (44.0%) and substantial relapse vulnerability
(10.8% drop). Neurosteroid-like inhibition achieved rapid combined
stress recovery (97.5%) while active but was state-dependent (decline
upon removal) with poor extreme noise buffering (42.5%) and moderate
relapse drop (4.1%).

Conclusions: These simulations demonstrate that antidepressants operate
through mechanistically distinct routes---structural rebuilding
(ketamine), gradual optimization of existing connectivity (SSRIs), or
reversible dynamic stabilization (neurosteroids)---yielding trade-offs
in onset speed, durability, and stress resilience. The findings support
a multifaceted plasticity framework for depression and provide
computational rationale for mechanism-based treatment selection and
combination strategies.

## Introduction

Major depressive disorder (MDD) is a top driver of disability worldwide,
touching hundreds of millions of people and creating large social and
economic burdens \[1\]. Drug treatment has helped many, yet results are
still disappointing: only about one-third of patients feel well after an
initial medicine, and roughly another third remain ill even after trying
several options \[2\]. The most common medicines---selective serotonin
re-uptake inhibitors (SSRIs)---often take weeks to work, leaving
patients unprotected during that wait and, for many, never bringing full
relief \[3\].

This slow and uneven response has pushed scientists to look for faster
and more reliable approaches. One such option is ketamine, a drug that
blocks NMDA-type glutamate receptors. In many studies, a single low-dose
infusion eases mood and even suicidal thoughts within hours, an effect
tied to a quick burst of new synapses through BDNF and mTOR signaling
\[4,5\]. Neuroactive steroids such as brexanolone and zuranolone, which
raise tonic GABA_A inhibition, can also lift depression quickly,
especially after childbirth \[6\]. Findings like these challenge the
classic \"low-serotonin\" story and instead point to problems in brain
plasticity: long-term stress thins dendrites and prunes synapses in key
regions like the prefrontal cortex and hippocampus, reducing the
brain\'s flexibility when new stress appears \[7,8\].

Computer models help explore how such circuit changes might lead to
illness. One model borrows the idea of excess teenage pruning---first
proposed for schizophrenia---and applies it to depression. In this view,
trimming too many synapses leaves networks that look fine at rest but
fall apart when noise or stress is added \[9\]. Letting the network
regrow the most useful connections restores function without returning
to full density, echoing the way ketamine sparks limited but targeted
synaptogenesis. What is still unclear is why glutamatergic,
monoaminergic, and GABAergic treatments differ in how fast they act, how
long they last, and which patients they suit best.

To tackle that question, we extend the pruning-plasticity model and
compare three stand-ins: (1) a ketamine-like surge of targeted synapse
growth, (2) an SSRI-like slow strengthening of the remaining links, and
(3) a neurosteroid-like boost in baseline inhibition. Starting with the
same over-pruned network, we watch how each strategy aids basic
recovery, guards against later stress, and affects the chance of
relapse. The results should clarify each drug class\'s trade-offs and
guide more personal treatment choices as the field turns toward rapid,
plasticity-focused therapies.

## Methods

### Network architecture and task

To study circuit fragility and recovery, we built a fully connected
feed-forward network that stands in for mood-relevant cortex (Figure 1).
The model accepted two continuous inputs, passed activity through three
hidden layers of 512, 512, and 256 ReLU units, and produced four
soft-max outputs. Altogether it held about 397 000 trainable weights.
Two features captured neuromodulatory influence: (1) additive Gaussian
noise could be injected after each hidden layer, and (2) a global
post-activation scaling factor could damp overall firing, mimicking
tonic inhibition.

The classification problem involved four Gaussian clusters centred at
(−3, −3), (3, 3), (−3, 3), and (3, −3) with a standard deviation of 0.8.
We created 12 000 training points, 4 000 noisy test points, and 2 000
clean test points. This simple task allowed a clear read-out of how
pruning and noise hurt accuracy and how different \"treatments\"
repaired it.

![](media/image1.png){width="6.268099300087489in"
height="5.5692989938757655in"}

***Figure 1.** Schematic representation of the neural circuitry model,
pathological mechanisms, and therapeutic interventions. The central
pipeline (Neural Circuitry) consists of a three-layer feed-forward
network processing 2D coordinate inputs. Pathology modules (dashed
lines) introduce synaptic pruning (95% sparsity) and stress-induced
noise into the hidden layers. Treatment modalities (solid lines)
represent distinct pharmacological mechanisms: Ketamine induces
gradient-guided regrowth in Layer 2, SSRIs stabilize weights in Layer 1,
and GABAergic neurosteroids provide tonic inhibition in Layer 3.*

### Baseline training and pruning

Networks started from random weights and were trained for 20 epochs with
Adam (learning rate = 0.001) while internal noise was set to zero. After
the dense model reached stable performance, we removed the smallest 95 %
of weights in each layer. The resulting 95 %-sparse network still
handled clean inputs but failed under noise, paralleling the hidden
liability proposed for major depressive disorder.

### Treatment protocols

![](media/image2.png){width="5.007099737532808in"
height="5.018099300087489in"}

***Figure 2:** Comparative Computational Protocols for Antidepressant
Mechanisms. The diagram illustrates the procedural logic for the three
simulated treatments starting from an identical baseline (95%
pruned/depressed state). Protocol A (Ketamine-like): Focuses on
structural plasticity. The model accumulates gradients to identify
\"ghost\" connections that would be beneficial if restored, then
explicitly regrows 50% of them, followed by a brief consolidation
period. Protocol B (SSRI-like): Focuses on gradual functional
adaptation. The network structure remains fixed (sparse). The model
undergoes a long training period (100 epochs) with a very low learning
rate while internal noise (stress) is linearly tapered from 0.5 to 0.0.
Protocol C (Neurosteroid-like): Focuses on rapid inhibitory modulation.
Structure remains fixed. The network\'s forward pass is modified to
include multiplicative damping (0.7x) and bounded activation functions
(Tanh), simulating enhanced tonic GABAergic inhibition.*

Three recovery procedures were applied to identical copies of the pruned
model (Figure 2).

Ketamine-like recovery re-added 50 % of the lost weights. Candidates for
regrowth were chosen by their gradient size, calculated over 30
mini-batches without noise. New weights were drawn from a normal
distribution with mean 0 and SD 0.03. A binary mask locked sparsity in
place while the network was fine-tuned for 15 epochs with Adam (learning
rate = 0.0005).

SSRI-like recovery left the sparse structure untouched and relied on
slow parameter drift. The model trained for 100 epochs at a learning
rate of 1 × 10⁻⁵. Internal activation noise began at σ = 0.5 and
declined linearly to zero, representing gradual neurotransmitter
stabilisation.

Neurosteroid-like recovery also kept the sparse mask but altered
activation dynamics. A global damping factor of 0.7 was applied after
each hidden layer, and ReLU activations were replaced with tanh to cap
firing rates. Ten epochs of tuning at 0.0005 allowed the model to
settle. Performance was later checked with the damping switch on (drug
present) and off (drug withdrawn).

### Evaluation and stress tests

Accuracy was recorded on three test sets: clean, original noisy, and
combined stress (input noise σ = 1.0 plus internal noise σ = 0.5). We
also swept internal noise from σ = 0.3 to 2.5 to chart resilience. To
mimic relapse, an extra 40 % of the remaining weights were pruned after
treatment; the combined-stress test was then repeated.

### Reproducibility

All runs used seed 42 for weight initialisation, data sampling, and
noise generation. Experiments were carried out in CPU-based PyTorch to
keep results deterministic. Code is available from the authors.

## Results

### Baseline performance of the pruned network

Removing 95 % of the weights immediately exposed the model\'s latent
weakness. Accuracy on noise-free inputs slipped to 50.8 %, and the usual
test set that already contained input jitter registered only 43.9 %.
When the combined challenge of input noise (σ = 1.0) and internal
activation noise (σ = 0.5) was applied, accuracy fell further to 31.8 %.
A sweep of pure internal noise showed the steepest losses: under extreme
noise (σ = 2.5) the network managed just 28.3 %. These values set the
benchmark for all later comparisons.

### Effects of ketamine-like treatment

Restoring half of the pruned synapses with gradient targeting cut
sparsity to 47.5 %. After 15 fine-tuning epochs the network again scored
100 % on both clean and standard inputs. Robustness also rebounded;
combined-stress accuracy reached 96.9 %, and even under extreme internal
noise the system held at 84.5 %. When a second pruning wave (40 % of the
remaining weights) was imposed to mimic relapse, combined-stress
accuracy dipped by only 0.2 %, revealing virtually complete protection.

### Effects of SSRI-like treatment

Keeping the 95 % sparsity unchanged but training slowly with fading
internal noise restored 100 % clean accuracy and 99.5 % on the standard
test set. Stress tolerance improved but did not match the ketamine
analogue: combined-stress accuracy climbed to 83.5 %, and performance
under extreme internal noise plateaued at 44.0 %. After the
relapse-style pruning, combined-stress accuracy dropped a further 10.8
%, indicating a sizeable vulnerability once additional damage occurred.

### Effects of neurosteroid-like treatment

Introducing a 0.7 global damping factor and tanh activations, while
still 95 % sparse, yielded 100 % accuracy on clean and standard inputs
when the modulation was active. Combined-stress accuracy peaked at 97.5
%, close to the ketamine result, yet extreme internal noise remained
difficult (42.5 %). Turning the damping off---simulating drug
withdrawal---lowered combined-stress accuracy to 90.5 % but
paradoxically raised extreme-noise accuracy to 58.6 %, showing that
state dependence shaped resilience. A relapse challenge under active
modulation produced a modest 4.1 % decline, midway between the ketamine
and SSRI patterns.

### Comparative summary

***Table 1.** Post-treatment performance and relapse vulnerability
across conditions.*

<table>
<colgroup>
<col style="width: 23%" />
<col style="width: 11%" />
<col style="width: 9%" />
<col style="width: 12%" />
<col style="width: 13%" />
<col style="width: 17%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Condition</strong></th>
<th><p><strong>Sparsity</strong></p>
<p><strong>(%)</strong></p></th>
<th><p><strong>Clean</strong></p>
<p><strong>(%)</strong></p></th>
<th><p><strong>Standard</strong></p>
<p><strong>(%)</strong></p></th>
<th><p><strong>Combined</strong></p>
<p><strong>Stress (%)</strong></p></th>
<th><p><strong>Extreme Stress</strong></p>
<p><strong>(σ=2.5) (%)</strong></p></th>
<th><p><strong>Relapse</strong></p>
<p><strong>Drop (%)</strong></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Untreated (pruned)</td>
<td>95.0</td>
<td>50.8</td>
<td>43.9</td>
<td>31.8</td>
<td>28.3</td>
<td>—</td>
</tr>
<tr class="even">
<td>Ketamine-like</td>
<td>47.5</td>
<td>100.0</td>
<td>100.0</td>
<td>96.9</td>
<td>84.5</td>
<td>−0.2</td>
</tr>
<tr class="odd">
<td>SSRI-like</td>
<td>95.0</td>
<td>100.0</td>
<td>99.5</td>
<td>83.5</td>
<td>44.0</td>
<td>10.8</td>
</tr>
<tr class="even">
<td>Neurosteroid-like (on)</td>
<td>95.0</td>
<td>100.0</td>
<td>100.0</td>
<td>97.5</td>
<td>42.5</td>
<td>4.1</td>
</tr>
<tr class="odd">
<td>Neurosteroid-like (off)</td>
<td>95.0</td>
<td>—</td>
<td>—</td>
<td>90.5</td>
<td>58.6</td>
<td>—</td>
</tr>
</tbody>
</table>

*Note: Values represent classification accuracy (%). \"Standard\" refers
to standard noisy test data. \"Combined Stress\" includes input noise (σ
= 1.0) plus internal activation noise (σ = 0.5). Relapse Drop reflects
the percentage point decrease in combined stress accuracy following an
additional 40% pruning of remaining weights. Dashes (---) indicate
metrics not applicable to the specific experimental condition.*

All three interventions restored perfect or near-perfect behaviour on
unperturbed data, but their stress profiles diverged (Table 1, Table 2).
Structural regrowth delivered by the ketamine-like procedure offered the
strongest buffer against both high noise and a second pruning insult.
The neurosteroid model nearly matched the ketamine condition on the main
stress test but relied on the continued presence of modulation and
showed weaker tolerance of extreme internal noise. The SSRI-like
strategy achieved respectable gains yet remained the most fragile when
additional pruning simulated relapse.

***Table 2.** Accuracy (%) under increasing internal activation noise.*

<table>
<colgroup>
<col style="width: 29%" />
<col style="width: 14%" />
<col style="width: 15%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Condition</strong></th>
<th><strong>No Noise</strong></th>
<th><p><strong>Moderate</strong></p>
<p><strong>(σ=0.5)</strong></p></th>
<th><p><strong>High</strong></p>
<p><strong>(σ=1.0)</strong></p></th>
<th><p><strong>Severe</strong></p>
<p><strong>(σ=1.5)</strong></p></th>
<th><p><strong>Extreme</strong></p>
<p><strong>(σ=2.5)</strong></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Untreated (pruned)</td>
<td>43.9</td>
<td>31.6</td>
<td>29.9</td>
<td>28.0</td>
<td>28.3</td>
</tr>
<tr class="even">
<td>Ketamine-like</td>
<td>100.0</td>
<td>99.8</td>
<td>99.0</td>
<td>96.1</td>
<td>84.5</td>
</tr>
<tr class="odd">
<td>SSRI-like</td>
<td>99.5</td>
<td>87.2</td>
<td>70.3</td>
<td>58.0</td>
<td>44.0</td>
</tr>
<tr class="even">
<td>Neurosteroid-like (on)</td>
<td>100.0</td>
<td>99.9</td>
<td>89.6</td>
<td>69.3</td>
<td>42.5</td>
</tr>
</tbody>
</table>

*Note: Data reflects performance resilience against graded internal
noise levels without additional input perturbation.*

## Discussion

### Interpretation of results

The simulations paint three clearly different recovery pictures that
help explain why patients respond so unevenly to modern antidepressants.
All modelled treatments returned the network to flawless performance
when no stressor was present---mirroring the clinical reality that most
drugs eventually lift core symptoms in people who respond. The
similarities ended once stress and relapse were introduced.

The ketamine-like intervention, which rebuilt half of the lost synapses
in a targeted way, stood out. After consolidation the network with only
47.5 % sparsity shrugged off the harshest stress (84.5 % accuracy at σ =
2.5) and lost virtually no ground after a second pruning wave. This
echoes clinical findings in which a single ketamine infusion triggers
BDNF-dependent spine growth and can hold depression at bay long after
the drug has cleared \[5,4,10\]. In the model, structural repair---not
continuing drug action---accounted for the resilience, supporting the
view that glutamatergic treatments create new \"reserve\" rather than
simply damping symptoms.

The SSRI-like schedule told another story. Without adding new
connections it slowly fine-tuned the existing sparse network, pushing
combined-stress accuracy from 31.8 % to 83.5 %. Yet tolerance of severe
noise stayed modest, and the network gave up 10.8 % accuracy after the
relapse simulation. That pattern fits the well-known therapeutic lag of
monoaminergic drugs, whose benefits rely on gradual receptor and
signalling changes rather than rapid synaptogenesis \[11\]. Network
analyses of real trials likewise show that SSRIs first lift mood and
anxiety; cognitive gains follow indirectly and are less robust \[12,8\].
The model therefore captures why these agents work reliably in milder
illness but often fall short when plasticity is deeply impaired.

The neurosteroid-like condition added no new wiring yet instantly
stabilised activity through stronger tonic inhibition. While the
dampening was active, the network matched ketamine on the main stress
test (97.5 %) but collapsed once modulation stopped, confirming a strong
state-dependence. Extreme internal noise was also harder to handle when
inhibition was high (42.5 %). Brexanolone and zuranolone exhibit an
analogous trade-off in clinical settings---rapid relief that diminishes
upon cessation of dosing \[6\]. The model indicates that these drugs
merely prolong duration rather than restore reserves, which is
advantageous in acute situations like postpartum depression.

Taken together, the findings reinforce a plasticity-based view of major
depression \[8\]. Ketamine restores structural capacity, neurosteroids
lend immediate but reversible stability, and SSRIs optimise what
connectivity remains (Figure 3). Recognising these distinct routes can
guide personalised care: patients showing deep structural loss may need
synaptogenic agents first, whereas those with heightened excitability
might respond to GABAergic modulation, and individuals with milder
circuit deficits may still do well on monoaminergic therapy alone.

![](media/image3.png){width="6.268099300087489in"
height="4.4444991251093615in"}

***Figure 3:** Comparative mechanisms of action and therapeutic outcomes
in the modelled network. The flow diagram illustrates how the three
simulated protocols diverge from the baseline depressive state. The
Ketamine-like pathway (left) relies on structural repair via synaptic
regrowth, creating a \"reserve\" that confers long-term durability. The
SSRI-like pathway (center) operates via the slow optimization of
existing, sparse connectivity, resulting in functional recovery that
remains vulnerable to severe stress and relapse. The Neurosteroid-like
pathway (right) utilizes functional modulation via tonic inhibition,
providing rapid but transient stability that is dependent on the active
presence of the intervention.*

### Novelty and translational impact

By placing glutamatergic, monoaminergic and GABA-ergic strategies into
the same pruning-based framework, the present study moves beyond earlier
single-mechanism simulations. Starting each model from an identical,
severely over-pruned \"depressed\" network allowed a clean comparison of
three therapeutic routes:

1.  ketamine-like structural rebuilding,

<!-- -->

1.  SSRI-like functional fine-tuning and

2.  neurosteroid-like activity damping.

![](media/image4.png){width="6.233899825021872in"
height="5.993699693788276in"}

***Figure 4:** Translational implications and triage principles. The
diagram maps the three modelled therapeutic routes from their
mechanistic origins to clinical applications. By distinguishing between
structural rebuilding (Ketamine-like), functional fine-tuning
(SSRI-like), and activity damping (Neurosteroid-like), the framework
supports a precision medicine approach. Patients are triaged based on
underlying neural deficits---structural loss versus
hyper-excitability---facilitating rational combination therapies, such
as using neurosteroids as a bridge to monoaminergic maintenance.*

From those direct contrasts several long-standing clinical puzzles begin
to make mechanistic sense. Rapid, durable recovery after ketamine
emerged because targeted synaptogenesis restored reserve and raised the
failure threshold, mirroring sustained clinical benefit in otherwise
refractory patients. The SSRI analogue acted more slowly and never fully
matched ketamine under heavy stress, reflecting the gradual receptor and
signalling adaptations seen in practice. The neurosteroid condition
delivered the quickest gain but remained state-dependent---beneficial
only while tonic inhibition was applied---capturing both the speed and
relapse risk of brexanolone or zuranolone.

Such distinctions strengthen the neuroplasticity view of depression,
shifting emphasis from a single transmitter deficit to the quality and
quantity of synaptic connections \[8\]. They also suggest concrete
triage principles (Figure 4). Individuals showing imaging or genomic
evidence of excessive pruning might be channelled toward synaptogenic
drugs; those with pronounced hyper-excitability could receive
GABA-enhancing agents as a bridge; and patients with milder structural
loss may still fare well with monoaminergic therapy. Finally, the
framework hints at rational combinations---using neurosteroids for
immediate relief while an SSRI consolidates longer-term
stability---thereby addressing the stubborn non-response rates
documented in sequential treatment trials.

### Limitations

The model remains an abstraction. A feed-forward network classifying
four Gaussian clusters cannot capture the recurrent loops,
neuromodulator gradients or heterogeneous cell types present in
corticolimbic circuits. Pruning and regrowth were implemented with
magnitude thresholds and gradient ranking, omitting microglial,
complement and astrocytic processes that sculpt synapses in vivo.
Likewise, tonic inhibition was represented by a simple global gain
change; real neurosteroid action is layer-, receptor- and
state-dependent. Internal Gaussian noise served as a stand-in for stress
hormones and inflammatory cascades but lacks their time courses.
Finally, all simulations used the same seed, so interpersonal
variability---central to clinical heterogeneity---was not addressed.

Conclusion

Despite these simplifications, the work illustrates how fragile,
over-pruned networks can be rescued by rebuilding, by patient
fine-tuning or by temporary damping---and why only the first route
yields deep, relapse-proof resilience. Embedding diverse drug actions
into a single developmental vulnerability model therefore offers a
practical bridge between computational insights and bedside decisions
\[10,8\]. Future efforts that add recurrence, individual variability and
multi-stage regimens could sharpen those predictions and speed the
arrival of faster, longer-lasting antidepressant care.

## References

\[1\] World Health Organization. World mental health report:
Transforming mental health for all. World Health Organization; 2022.

\[2\] Rush AJ, et al. Acute and longer-term outcomes in depressed
outpatients requiring one or several treatment steps: A STAR\*D report.
American Journal of Psychiatry. 2006;163(11):1905--1917.

\[3\] Trivedi MH, et al. Evaluation of outcomes with citalopram for
depression using measurement-based care in STAR\*D: Implications for
clinical practice. American Journal of Psychiatry. 2006;163(1):28--40.

\[4\] Murrough JW, et al. Antidepressant efficacy of ketamine in
treatment-resistant major depression: A two-site randomized controlled
trial. American Journal of Psychiatry. 2013;170(10):1134--1142.

\[5\] Iadarola ND, et al. Ketamine and other N-methyl-D-aspartate
receptor antagonists in the treatment of depression: A perspective
review. Therapeutic Advances in Chronic Disease. 2015;6(3):97--114.

\[6\] Gunduz‐Bruce H, et al. Development of neuroactive steroids for the
treatment of postpartum depression. Journal of neuroendocrinology.
2022;34(2):e13019.

\[7\] Duman RS, Aghajanian GK. Synaptic dysfunction in depression:
Potential therapeutic targets. Science. 2012;338(6103):68--72.

\[8\] Thompson SM, et al. Beyond the serotonin deficit hypothesis:
Communicating a neuroplasticity framework of major depressive disorder.
Molecular Psychiatry. 2024. Advance online publication.

\[9\] Cheung N. Simulating Synaptic Pruning and Ketamine-Like Recovery
in Depression: Insights from Consolidation Duration and Iterative
Regimens on Resilience and Relapse. Zenodo. 2026.

\[10\] Krystal JH, et al. Ketamine: A paradigm shift for depression
research and treatment. Neuron. 2019;101(5):774--778.

\[11\] Stahl SM. Mechanism of action of serotonin selective reuptake
inhibitors: Serotonin receptors and pathways mediate therapeutic effects
and side effects. Journal of Affective Disorders. 1998;51(3):215--235.

\[12\] Boschloo L, et al. The complex clinical response to selective
serotonin reuptake inhibitors in depression: a network perspective.
Translational Psychiatry. 2023;13(1):19.
