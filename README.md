# Trader-Behavior-Insights
Crypto Trading Analytics and Behavioral Archetypes

This project explores cryptocurrency trading behavior by combining market sentiment (Fear & Greed Index) with historical trading data to uncover:

Performance patterns

Behavioral biases

Distinct trader archetypes

The objective is to generate actionable insights and strategy recommendations for navigating different market conditions.

Methodology
1. Data Acquisition & Preprocessing
Datasets Used

Fear & Greed Index dataset

Columns: timestamp, value, classification, date

Historical trading dataset

Detailed trade-level transaction records

Cleaning & Transformation
Fear & Greed Index

Dropped the value and timestamp columns

Merged:

Extreme Fear → Fear

Extreme Greed → Greed

Converted date to datetime and extracted only the date component

Historical Trading Data

Dropped redundant columns:

Transaction Hash

Unix Timestamp

Converted Timestamp IST to datetime

Extracted date component

Data Integration

Performed a right merge on Date

Ensured every trade is associated with a market sentiment label

Final dataset: final_df

2. Performance & Behavioral Feature Engineering

For each trading account, the following metrics were computed:

Total Profit & Loss (PnL)

Win rate

Average trade size (USD)

Total number of trades

Number of winning trades

Long/short bias (Buy vs Sell ratio)

Sentiment Exposure

Calculated proportion of trades under:

Fear

Greed

Neutral

Used dummy variable encoding

3. Trader Segmentation & Analysis
Feature Preparation

Created trader_features summarizing all engineered metrics per account

Feature Scaling

Applied StandardScaler to normalize numerical values

Clustering

Used Silhouette Score to determine optimal clusters

Identified 7 trader archetypes using K-Means

Archetype Interpretation

Analyzed cluster centroids (scaled & unscaled) to understand:

Performance

Behavior

Sentiment exposure

Visualization

Applied PCA (2D reduction)

Generated scatter plot of trader archetypes

Key Insights
1. Performance Variation by Market Sentiment
Greed

Highest total PnL: $4.87M

Highest win rate: 42.03%

Highest total loss: –$1.33M
➡ Indicates high opportunity + high risk

Fear

Largest average loss per losing trade: –$196.35

Still strong total PnL: $4.10M
➡ Skilled traders can profit despite volatility

Neutral

Lowest activity and profitability

Total PnL: $1.29M

Win rate: 39.70%

Avg loss: –$121.73
➡ Represents low-momentum market

2. Behavioral Adaptation to Sentiment
Trade Frequency

Greed → 90,295 trades

Fear → 83,237 trades

Neutral → 37,686 trades

Position Sizes

Highest during Fear: $7,182
➡ Fewer trades but larger conviction bets

Long/Short Bias

Slight SELL bias in both Fear & Greed
➡ Suggests:

Profit-taking in rallies

Defensive positioning in downturns

3. Trader Archetypes (7 Clusters)
High-Profit, Large-Bet Traders (Cluster 6)

Avg PnL: $1.87M

Avg trade size: $10K

High-Activity, Fear-Prone Traders (Cluster 4)

Avg trades: 30,688

Avg PnL: $888K

Strong Fear exposure

High-Win-Rate, Greed-Oriented Traders (Cluster 0)

Win rate: 59.7%

Avg PnL: $259K

Strong Greed exposure

Remaining Clusters

Represent combinations of:

Win rate

Trade size

Long/short bias

Sentiment exposure
➡ Demonstrating diverse trading behaviors

Strategy Recommendations
1. Dynamic Position Sizing in Fearful Markets

Rule of Thumb

High-performing traders may increase position sizes on high-conviction trades

Must combine with strict risk management (tight stop-losses)

Low-PnL traders should remain cautious

Justification

High-PnL traders stay profitable in Fear ($66.38 avg PnL)

Largest position sizes occur in Fear ($7,182)

Highest losing-trade loss: –$196.35

2. Optimized Trading in Greedy Markets

Rule of Thumb

Increase trading activity during Greed

Consider:

Profit-taking on longs

Careful short positions

Low-profit traders should manage downside risk

Justification

Highest trade frequency: 90,295

Highest total PnL: $4.87M

Slight SELL bias observed

Largest total losses: –$1.33M
