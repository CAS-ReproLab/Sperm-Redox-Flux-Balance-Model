# Sperm-Redox-Flux-Balance-Model
A constrained linear optimization model to accompany the article: "Pyruvate modulation of redox potential governs mouse sperm motility "
# Constrained Linear Optimization Modeling

To estimate how specific metabolic network states relate energetically to sperm mechanical function, a constrained linear optimization model was developed in conjunction with empirical data. This approach aims to incorporate information regarding dynamics of the metabolic network and compare it with kinematic efficiency[^34][^61].

## Methodology

Briefly, this method assumes that unknown metabolic reaction fluxes can be estimated from a set of known (experimentally determined) fluxes if the stoichiometric coefficients of the network are known. Additionally, the fluxes are assumed to be 'mass balanced' under a steady state condition. The steady state metabolic flux condition was defined as:

\[
S \cdot v = 0
\]

where \( S \) and \( v \) denote the stoichiometric matrix and the vector of net reaction rates (pmol/min/μg protein) respectively.

Non-negativity constraints and boundary constraints were incorporated into the model using empirical data obtained from several experiments in this study:

\[
0 \leq v_i
\]
\[
v_{lb} \leq v_i \leq v_{ub}
\]

where \( v_i \) denotes the \( i^{th} \) reaction flux, and \( v_{lb} \) and \( v_{ub} \) are the upper and lower flux bounds respectively.

The objective function was designed to maximize the rate of flux through all reactions in the network:

\[
\text{maxObj}(s,v) = \sum c_i v_i
\]

where \( c_i \) represents the \( i^{th} \) flux weight (assigned one in all cases in this report).

Solutions were obtained using the `linprog` function from the Matlab optimization toolbox. The `normrnd` function was used to generate random numbers from Gaussian distributions with means and standard deviations determined from our empirical measurements.

## Kinematic Efficiency

Kinematic efficiency was defined as:

\[
K_E = \frac{VCL}{f}
\]

where \( VCL \) is curvilinear velocity, or the average velocity measured over the actual point-to-point track followed by the cell (μm/sec), and \( f \) is beat cross frequency in Hz. \( K_E \) denotes the distance traveled per the frequency with which the sperm's head crosses the average path.

## Oligomycin A1 Titrations

Oligomycin A1 titrations were used to determine the apparent coupling efficiency (\( Q_{\text{eff}} \)) of oxidative phosphorylation in intact sperm. Apparent coupling efficiency was defined as:

\[
Q_{\text{Eff}} = \frac{(JO_{2,\text{init}} - JO_{2,\text{oligo}})}{(JO_{2,\text{init}})}
\]

Where \( JO_{2,\text{init}} \) is the initially measured oxygen consumption rate and \( JO_{2,\text{oligo}} \) is measured following titration of oligomycin (50 nM up to ~200 nM). \( Q_{\text{Eff}} \) represents the quantity of respiration that is 'sensitive' to inhibition of ATP synthase.

Respiration that remains is coupled with other dissipative processes such as electrogenic transport, uncoupling protein activity, etc. In the linear optimization model, \( Q_{\text{Eff}} \) was used as a correction factor for the ATP:O ratio (2.65), resulting in a final ATP:O ratio of 1.58 for NADH-linked respiration.
