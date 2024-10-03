# DT-GEO WP5 DTC-V4: Volcanic gas dispersal and deposition
## News
 - 2024/09/02 ST540202, ST540203, ST540204, ST540206 betas released
 - 2024/03/05 SS5401 beta released

## Workpackage structure
Building blocks for DT-GEO work package 5 Digitial Twin Component 4, "Volcanic gas dispersal and deposition"
- SS5401 fetch_amd_simulate.py
- SS5403 watch_and_fetch.py
- SS5404 train.py
- SS5405 infer.py
- SS5406 fit.py
- SS5407 corect_forecast_visualise.py
  
For further details see DTC-V4 workflow requirements revised.docx
<a href="url"><img src="https://raw.githubusercontent.com/profskipulag/.github/main/diagram_full.jpg" align="left" height="1000" ></a>

## Overview
This DTC estimates the posterior joint distribution over volcanic plume height, volcanic $SO_2$ flux, and $SO_2$​ concentration at ground level from sparse observations of these variables and an atmospheric dispersion model. The posterior is specified by a hierarchical Bayesian model implemented in the Stan probabilistic programming language, from which samples are drawn using Hamiltonian Monte Carlo. These samples are then used to estimate marginal density distributions over parameters of interest, as well as threshold exceedence probabilities, which are displayed on time series plots and maps on an interactive website implemented in D3.js with a python FastAPI backend. In addition to the posterior distribution, individual samples (similar to a particular scenario in an ensemble) can be selected and plotted, to see what an individual outcome might look like, in comparison to the probability distribution over all outcomes.


The relationship between the plume height and flux (which taken together are called Eruption Source Parameters, or ESPs) and the ground concentrations is given by an atmospheric dispersion model. Here we use Fall3D, however as the HMC scheme requires many thousands of forward runs we replace it with an Emulator, a function that approximates the model but runs much faster. So far, we have implemented a simple interpolate-scale-sum emulator that leverages the linear relationship between flux and ground concentration for basic Fall3D runs and gives adequate results. However, we are working on more sophisticated neural network based solutions that are more generally applicable. The use of an emulator also allows the user to interact with it in real time, so we have added functionality to the website that allows the user to alter the plume height or flux for a specific time and see in near real time the change in forecast ground concentrations on the map, to give an idea of the sensitivity or to allow investigation of scenarios deemed unlikely by the model for one reason or another.

In using emulators within a Bayesian framework we are adopting the philosophy of "emulate deterministic relationships, and sample stochastic ones". The idea is to treat the time evolution of the state of the volcano as our parameter space, and use emulators to calculate all variables (e.g. estimates of measured environmental parameters) that follow deterministically. In this way we can compose emulators together to represent different combinations of physical processes within flexible, sophisticated statistical models that can still be sampled adequately in reasonable time. As an example of this flexibility, we are experimenting with adding empirical relationships between plume height and ambient weather conditions identified inthe 2021 Fagradalsfjall eruption, which will aid with the forecasting element of this DTC (i.e. the posterior distribution over ground concentrations beyond the last observations incorporated into the model)

<!--
#![Alt text](diagram_full.jpg?raw=true "Optional Title")




**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
