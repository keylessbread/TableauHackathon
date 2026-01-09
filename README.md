🏨 Hotel Price Optimization: 
Latent Space & Dilution AnalysisThis tool provides a revenue management framework for analyzing sparse pricing data in a 124-room hotel environment. Instead of treating unoccupied rooms as null values or zeros—which distorts price distributions—this model maps vacancies into a Standard Normal Distribution to quantify the "Dilution Effect."

📊 Matrix Architecture
The core data structure is a 6x30 Matrix (Room Types vs. Days of June 2025):The Conditional Space: Represents "Realized Revenue" (only occupied rooms).The Full Vector Space: Accounts for all 124 rooms by expanding the conditional matrix and identifying the "Occupancy Gap."Z-Score Imputation: To maintain statistical integrity, unoccupied rooms are not filled with $0$, but are imputed as $-1.96$ (representing the 2.5th percentile "shadow" of the price distribution).🛠 Key Methodologies1. The Dilution TransformationWe define the relationship between the successful sales (Conditional) and the total capacity (Full Space) as a Scaling Transformation ($S$).

The Problem: High gross prices often mask a "Dilution Effect" where low occupancy results in a lower net mean than intended.

The Solution: By standardizing the matrix, we visualize "Market Drag"—areas where the price is statistically too far from the mean to generate volume.2. Inverse Scalar Price RecommendationTo solve for optimal occupancy, the tool calculates an Inverse Scalar ($S^{-1}$). This functions as a "Correction Nudge" to bring the underperforming room varieties back into the market-clearing range.$$P_{rec} = \mu_{cond} - \left( \frac{1.96 \cdot (1 - Occ)}{Occ} \right) \cdot \sigma_{cond}$$

💻 Implementation Overview
The repository contains two primary algorithmic approaches:Probabilistic Imputation (NumPy/Pandas): Standardizes room-type vectors and fills the "latent space" with Z-scores to prepare data for visualization.Linear Programming (SciPy/PuLP): An optimization suite that maximizes the Contribution Margin (Price minus Variable Costs) across all 30 days while respecting capacity and demand constraints.

📈 Visualization with Tableau
The output is optimized for Tableau "Long-Format" data, enabling: 
  - Quadrant Analysis: Identifying "Overpriced/Low-Occ" vs "Underpriced/High-Occ" rooms.
  - Vector Field Mapping: Visualizing the distance between current pricing and the "Equilibrium Price" required for full occupancy.
