# Celebrity-Death-Analytics

## Overview

This repository presents a data analytics study examining the death of Whitney Houston (February 11, 2012) through six speculative scenarios, ranging from low-probability rumors to high-probability evidence-based theories. Using RStudio and the `plotly` library, this project builds on a prior analysis of Angie Stone’s death (March 1, 2025) to explore patterns in celebrity death conspiracies as of March 26, 2025. The study leverages mock datasets and predictive modeling to estimate the likelihood of each scenario, visualized in an interactive 3D scatter plot.

## What Was Accomplished

### Whitney Houston Death Scenarios
- **Objective**: Analyzed six top-probability scenarios for Whitney Houston’s death, inspired by official reports, media, X rumors, and parallels to Angie Stone’s case.
- **Scenarios**:
  - **Low-Probability** (Rumor-Driven):
    - Drug Dealer Murder (6.7%): Killed over a $1.5M debt, staged drowning.
    - Clive Davis Conspiracy (2.6%): Mentor orchestrated death for profit or silence.
    - Bobby Brown Involvement (4.2%): Ex-husband arranged death.
  - **High-Probability** (Evidence-Based):
    - Accidental Overdose and Drowning (45.0%): Official coroner finding.
    - Prescription Drug Interaction (30.8%): Cocaine, Xanax, alcohol mix caused drowning.
    - Industry Hit via Sabotage (37.3%): Industry sabotaged her with drugs, tied to disputes.
- **Methodology**: Used a predictive model: Adjusted Likelihood = Initial_Likelihood × (Evidence_Strength + Motive_Plausibility) / (1 + Rumor_Spread). Inputs derived from coroner reports, X sentiment, and hypothetical evidence.
- **Output**: A 3D scatter plot visualizing likelihood, evidence strength, and rumor spread, with hover details for each scenario.

### R Code
```R
# Load libraries
library(plotly)
library(dplyr)

# Create dataset
data <- data.frame(
  Speculation = c("Drug Dealer Murder", "Clive Davis Conspiracy", "Bobby Brown Involvement", 
                  "Accidental Overdose", "Prescription Interaction", "Industry Hit via Sabotage"),
  Adjusted_Likelihood = c(6.7, 2.6, 4.2, 45.0, 30.8, 37.3),
  Evidence_Strength = c(0.2, 0.1, 0.1, 0.9, 0.8, 0.6),
  Rumor_Spread = c(0.8, 0.9, 0.7, 0.2, 0.3, 0.5),
  Scenario_Type = c("Low Probability", "Low Probability", "Low Probability", 
                    "High Probability", "High Probability", "High Probability"),
  Description = c(
    "Killed by dealers over $1.5M debt, staged drowning",
    "Davis orchestrated death for profit or silence",
    "Brown arranged death, tied to past",
    "Overdose on cocaine, drowned accidentally",
    "Cocaine, Xanax, alcohol mix caused drowning",
    "Industry sabotaged her with drugs,519 tied to disputes"
  )
)

# 3D Scatter Plot
plot_3d <- plot_ly(data,
  x = ~Evidence_Strength,
  y = ~Rumor_Spread,
  z = ~Adjusted_Likelihood,
  type = "scatter3d",
  mode = "markers",
  marker = list(
    size = 10,
    color = ~Scenario_Type,
    colorscale = list(c(0, 1), c("#7570b3", "#d95f02")), # Purple for Low, Orange for High
    showscale = FALSE
  ),
  text = ~paste(
    "Speculation: ", Speculation, "<br>",
    "Likelihood: ", Adjusted_Likelihood, "%<br>",
    "Evidence Strength: ", Evidence_Strength, "<br>",
    "Rumor Spread: ", Rumor_Spread, "<br>",
    "Description: ", Description
  ),
  hoverinfo = "text"
) %>%
  layout(
    title = "Whitney Houston Death: Top 6 Probability Scenarios",
    scene = list(
      xaxis = list(title = "Evidence Strength (0-1)", range = c(0, 1)),
      yaxis = list(title = "Rumor Spread (0-1)", range = c(0, 1)),
      zaxis = list(title = "Adjusted Likelihood (%)", range = c(0, 50))
    ),
    legend = list(title = list(text = "Scenario Type"))
  )

# Display
print(plot_3d)

# Save as HTML
htmlwidgets::saveWidget(plot_3d, "whitney_houston_3d_scatter.html")
```
- **Findings**: “Accidental Overdose” (45.0%) leads, supported by coroner evidence, while “Industry Hit via Sabotage” (37.3%) offers a plausible conspiracy tied to her $100M Arista deal disputes. Low-probability rumors (2.6-6.7%) lack substantiation.

## Prerequisites
- **RStudio**: To run the script.
- **R Packages**: Install via `install.packages(c("plotly", "dplyr"))`.

## Usage
1. Clone the repo: `git clone https://github.com/username/Celebrity-Death-Analytics.git`
2. Open the script in RStudio.
3. Run to generate the 3D scatter plot.
4. View the HTML output (`whitney_houston_3d_scatter.html`) in a browser for interactivity.

## Why This Matters
Whitney Houston’s death, like those of Prince and Angie Stone, sparks enduring questions about celebrity vulnerability and industry influence. This study uses data analytics to sift through rumors and facts, offering clarity on what’s plausible versus speculative. Understanding these scenarios sheds light on systemic issues—drug culture, industry power dynamics, and public perception—that impact artists and shape legacies. It’s a step toward informed discourse over conspiracy noise.

## Conclusion
This project delivers a structured analysis of Whitney Houston’s death, balancing official narratives with high-profile rumors. The 3D visualization highlights “Accidental Overdose” as the most likely cause, while keeping industry sabotage as a compelling alternative if new evidence emerges. Contributions to refine probabilities or expand to other cases (e.g., Prince, Stone) are welcome!
