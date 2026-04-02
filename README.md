# Capturing Tail Risks in the Carbon Emission Allowance Returns Using Kernel Density Estimation

## Description
Traditional risk metrics often struggle with the "heavy tails" of carbon price swings. This project moves beyond standard Gaussian assumptions by applying Kernel Density Estimation (KDE) to Value-at-Risk (VaR) modelling. By analysing different market phases, this tool offers deeper insights into the extreme price risks of European Union Allowances (EUA), helping carbon-exposed industries better prepare for market volatility.

## Key Features
-	Non-parametric Risk Modelling: Using KDE to relax distributional assumptions, allowing for a more precise capture of heavy-tailed distributions and extreme market shocks.
-	Phase-specific Analysis: Evaluating risk evolution across EU ETS regulatory phases (Phase 2 to Phase 4) to identify how policy shifts and market maturity impact price volatility.
-	Advanced Risk Metrics: Quantifying risk through 95% VaR, Expected Shortfall (ES), and ES-to-VaR ratios, providing deeper insights into the severity of losses beyond the confidence threshold. 

## Data Setup 
### Data Overview
The analysis utilised historical EUA daily price data, characterised by the following:
-	Source: Bloomberg Terminal (EU ETS Transactions).
-	Period: January 2008 – May 2024.
-	Currency: Euro (€).

### Policy-Driven Segmentation
Since the EUA prices are heavily influenced by regulatory shifts rather than stochastic process, the data was segmented based on the stages of the EU ETS:
-	Phase 1 (2005 - 2007)
-	Phase 2 (2008 - 2012)
-	Phase 3 (2013 - 2020)
-	Phase 4 (2021 - Present)

>[!Important]
>-	Price data from Phase 1 (2005 - 2007) was excluded from the analysis due to nascent market demand and low transaction volumes, which do not reflect current market liquidity.
>-	Phase 3 (2013 - 2020) was further divided into Pre-2016 and Post-2016 subphases to account for the introduction of the Market Stability Reserve (MSR) proposal.

## Data Transformation
Raw daily prices were converted into simple returns to standardise market volatility. In this analysis, positive returns (right-tail risk) were considered as the primary risk factor, reflecting the financial strain that surging EUA prices impose on carbon-intensive industries.

## Privacy Disclaimer 
>[!warning]
>To comply with Bloomberg’s data licensing and privacy constraints, the raw dataset is not included in this repository. All code and outputs are provided for methodological demonstration purposes only.

## Methodology
### KDE Parameter 
| Parameter | Technical Specification | Statistical Rationale |
| :--- | :--- | :---|
| Gaussian Kernel | $$K(u)=\frac{1}{\sqrt{2\pi}}\exp\left(-\frac{u^2}{2}\right)$$| Chosen for its mathematical properties, which simplify bandwidth selection.|
| Bandwidth Selection | Sheater-Jones Plug-in Method | Minimises the Asymptotic Mean Integrated Squared Error (AMISE) for optimal fit.|


### Risk Metrics Calculation
The top 10% of returns were first isolated to reduce the influence of the central part of the distribution on the estimation results.
| Risk Metric | Technical Implementation |
| :--- | :--- |
| VaR | Derive the median of the extreme upper decile (top 10%) using KDE-derived densities.|
| ES | Calculate the average magnitude of extreme returns beyond VaR.| 

### Backtesting
The Kupiec test is a backtesting method specifically designed for VaR models. It examines whether the number of observed EUA returns exceeding the VaR is consistent with the number predicted by the model.

# Visualisations
![KDE Right Tails](figures/kde_right_tails.png)
![Tail Risk Plots](figures/tail_risk_plots.png)
![VaR and ES](figures/var_es.png)
