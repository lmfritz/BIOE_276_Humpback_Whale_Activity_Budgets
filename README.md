# BIOE 176/276 Final Project
## Distinguishing Behavioral State Allocations for Whales with Calves on the Antarctic Foraging Ground

### Motivating Question

We want to understand if whales with calves, which are presumed to be female and the mother of the calf, alter their activity budget on the foraging ground to account for the energetic demands of rearing offspring.

More specifically, this project asks:

How do humpback whales with a calf present allocate their time among behavioral states during the Antarctic foraging season, and how do these behavioral state allocations compare to whales without calves?

Understanding how behavioral activity budgets differ between demographic groups can provide insight into energetic tradeoffs and ecological constraints experienced during the critical Antarctic feeding season.

### Rationale for the Question

There has been extensive study of the foraging behavior of Antarctic humpback whales along the Western Antarctic Peninsula, but relatively little work examining how behavior varies among different whale demographic groups.

This project uses a decade-long dataset of CATS (Customized Animal Tracking Solutions) tag data collected by the Biotelemetry and Behavioral Ecology Lab and collaborators. These high-resolution datasets allow researchers to quantify whale movement and classify behavioral states.

Analyzing behavioral state allocations across demographic groups provides an opportunity to better understand how the energetic demands of reproduction influence activity budgets during the foraging season.

# Target Audience

Academic community of polar marine ecologists and marine biologists interested in behavioral ecology, marine mammal energetics, and Antarctic ecosystem dynamics.

# Repository Structure

This repository contains the full workflow for analyzing humpback whale behavioral state allocations.

Files include:

- Motivation_for_Study.qmd – background and motivating question
- Data Wrangling.qmd – data cleaning and preparation
- Model.qmd – statistical analysis using brms
- DAGS2.qmd – causal diagram used to guide modeling decisions
- Whale_Data_Filtered.csv – cleaned dataset used for modeling
- EEB 276 Final Project.csv – original dataset

## Dataset Metadata

Dataset: Whale_Data_Filtered.csv

Source:
Biotelemetry and Behavioral Ecology Lab (BTBEL)

Variables:
- Group – demographic group (e.g., calf present or not)
- Resting_min – minutes spent resting
- Traveling_min – minutes spent traveling
- Foraging_min – minutes spent foraging
- Exploring_min – minutes spent exploring
- total_min – total behavioral observation time

Units:
Behavioral states are measured in minutes of observation time.

## Hypotheses

H1: Whales with calves allocate more time to resting behavior compared to whales without calves.

H2: Whales with calves allocate less time to active behaviors such as traveling or exploring.

H3: Behavioral time allocation varies across the Antarctic foraging season.

### Background

**Scientific Motivation:**

Understanding how animals allocate time between behavioral states is a central goal in behavioral ecology, particularly for large migratory marine mammals whose foraging opportunities are spatially and temporally constrained.

For humpback whales, the Antarctic foraging season is a critical period during which individuals must acquire sufficient energetic reserves to support migration and reproduction throughout the rest of the year. Behavioral states commonly observed during this period include traveling, resting, foraging, and exploring.

Most studies of humpback whale behavior in this region have focused primarily on foraging behavior. Less attention has been given to how time is allocated among other behavioral states or how these allocations vary across demographic groups.

By quantifying the proportion of time spent in each behavioral state, this project aims to establish a baseline description of activity budgets for Antarctic humpback whales and to examine whether whales with calves display different behavioral patterns than other individuals.

**Data Overview:**

For this analysis we use high-resolution multi-sensor data collected via CATS tags during Antarctic humpback whale field seasons from 2012–2025 along the Western Antarctic Peninsula.

Sixty-five tag deployments from 2015–2022 were available from the Biotelemetry and Behavioral Ecology Lab database. Additional deployments from later years may be incorporated in future analyses.

Data streams include measurements of:
- depth
- movement
- orientation
These data allow classification of whale behavior into four broad behavioral states:
- Resting
- Traveling
- Foraging
- Exploring

Activity budgets are estimated by calculating the proportion of time individuals spend in each behavioral state during tag deployments.

Only deployments meeting established quality and duration criteria were included in the analysis to ensure consistency across individuals and years.

**Behavioral Classification Framework:**

Behavioral states were defined to capture major modes of whale activity while maintaining interpretability across individuals and deployments.

The four behavioral states analyzed in this project include:

- Resting – periods of minimal movement and low activity.
- Traveling – sustained directional movement.
- Foraging – behaviors associated with feeding activity.
- Exploring – active, non-directional movement that does not clearly fall into traveling or foraging categories.

The exploring category functions as a residual behavioral state that captures activity not easily classified into other behavioral types.

Additional exploratory analyses evaluate whether the exploring category contains multiple dive types distinguishable by basic dive characteristics such as depth and duration.

**Update to Behavioral State Allocation – Further Analysis of “Exploring”**

Recent discussions have highlighted the importance of assessing whether the exploratory behavioral state encompasses multiple dive types distinguishable by basic dive characteristics (e.g., depth and duration). We will conduct a constrained, descriptive analysis to evaluate potential heterogeneity within the “exploring” category. This assessment is intended to serve as a validation step and test the robustness of the existing behavioral framework rather than redefine behavioral states or infer fine-scale foraging or energetic processes.

**Analytical Approach:**

Activity budgets were estimated by quantifying the proportion of time individuals allocate to each behavioral state across tag deployments.

The primary comparison examines differences in behavioral state allocation between whales with and without calves.

By examining how time is distributed among behavioral states across demographic groups, this analysis evaluates whether the energetic demands of calf care influence whale behavior during the Antarctic feeding season.

# Statistical Analysis

Behavioral state allocations were modeled using Bayesian regression approaches implemented in the brms package in R.

Two complementary modeling approaches were used to analyze the activity budget data.

## Multinomial Regression

A multinomial model was used to evaluate how the distribution of time across behavioral states varied by whale group type. This model treats behavioral states as competing outcomes within a fixed time budget and estimates how the relative probability of each state changes across demographic groups.

Model structure:
cbind(Resting_min, Traveling_min, Foraging_min, Exploring_min) | trials(total_min) ~ Group
This approach allows simultaneous comparison of the proportion of time allocated to each behavioral state across whale demographic groups.

## Beta Regression

Because behavioral time allocation can also be represented as proportions, a beta regression model was additionally used to evaluate differences in the proportion of time spent in individual behavioral states.

Beta regression is appropriate for continuous response variables bounded between 0 and 1, making it well-suited for modeling proportional activity budgets.

Using both modeling approaches provides complementary perspectives on the data and allows evaluation of whether patterns are consistent across different statistical frameworks.

## Model Evaluation
Model performance and fit were assessed using several standard Bayesian diagnostic tools within the brms package.

These included:
- Posterior predictive checks to evaluate whether simulated data from the model resembled observed data.
- Credible intervals for model parameters to determine the strength and direction of estimated effects.
- Convergence diagnostics, including R-hat values and effective sample sizes, to confirm proper Markov Chain Monte Carlo sampling.
Both the multinomial and beta regression models were evaluated using these diagnostics to ensure reliable parameter estimation and model stability.

# Key Findings

Preliminary results suggest that whales observed with calves exhibit differences in behavioral time allocation compared to whales without calves.

In particular, whales with calves appear to allocate a greater proportion of time to resting and less to active behaviors such as traveling or exploring. These differences likely reflect the energetic constraints associated with lactation and calf care during the Antarctic feeding season.

Further analyses will help clarify how these behavioral differences vary across the season and among individual deployments.

# Conclusions

Characterizing activity budgets provides important ecological context for understanding the behavioral strategies humpback whales use during the Antarctic foraging season.

Differences in behavioral state allocation between whales with calves and those without calves suggest that reproductive status may influence how individuals balance foraging, movement, and recovery behaviors.

Establishing these baseline patterns helps improve our understanding of humpback whale behavioral ecology and provides a reference framework for future studies examining energetic demands, environmental variability, and potential disturbance impacts on Antarctic whale populations.
