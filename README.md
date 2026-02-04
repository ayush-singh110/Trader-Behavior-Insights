# 📊 Crypto Trading Analytics & Behavioral Archetypes

A data-driven exploration of cryptocurrency trading behavior combining market sentiment analysis with historical trading patterns to uncover performance metrics, behavioral biases, and distinct trader archetypes.

## 🎯 Project Overview

This project analyzes cryptocurrency trading behavior by integrating:
- **Market Sentiment Data**: Fear & Greed Index
- **Historical Trading Records**: Transaction-level data

**Objectives:**
- Identify performance patterns across market conditions
- Uncover behavioral biases in trading decisions
- Segment traders into distinct behavioral archetypes
- Generate actionable trading strategy recommendations

---

## 📋 Table of Contents

- [Methodology](#methodology)
- [Key Insights](#key-insights)
- [Trader Archetypes](#trader-archetypes)
- [Strategy Recommendations](#strategy-recommendations)
- [Installation & Usage](#installation--usage)
- [Data Schema](#data-schema)
- [Results Visualization](#results-visualization)

---

## 🔬 Methodology

### 1. Data Acquisition & Preprocessing

#### **Datasets Used**

**Fear & Greed Index Dataset**
- Columns: `timestamp`, `value`, `classification`, `date`

**Historical Trading Dataset**
- Detailed trade-level transaction records

#### **Data Cleaning & Transformation**

**Fear & Greed Index:**
```python
# Dropped: value, timestamp columns
# Merged classifications:
#   - Extreme Fear → Fear
#   - Extreme Greed → Greed
# Converted date to datetime (date component only)
```

**Historical Trading Data:**
```python
# Dropped redundant columns:
#   - Transaction Hash
#   - Unix Timestamp
# Converted Timestamp IST to datetime
# Extracted date component
```

#### **Data Integration**
- Performed **right merge** on `Date`
- Ensured every trade has an associated market sentiment label
- Final dataset: `final_df`

---

### 2. Performance & Behavioral Feature Engineering

For each trading account, computed:

| Metric | Description |
|--------|-------------|
| **Total PnL** | Cumulative profit/loss |
| **Win Rate** | Percentage of profitable trades |
| **Avg Trade Size** | Average position size (USD) |
| **Total Trades** | Number of transactions |
| **Winning Trades** | Count of profitable positions |
| **Long/Short Bias** | Buy vs Sell ratio |

#### **Sentiment Exposure Analysis**
Calculated proportion of trades executed under:
- Fear
- Greed  
- Neutral

Used dummy variable encoding for categorical analysis.

---

### 3. Trader Segmentation & Clustering

#### **Feature Preparation**
- Created `trader_features` summarizing all metrics per account

#### **Feature Scaling**
- Applied `StandardScaler` for normalization

#### **Clustering Algorithm**
- Used **Silhouette Score** to determine optimal cluster count
- Identified **7 distinct trader archetypes** using K-Means

#### **Archetype Analysis**
- Analyzed cluster centroids (scaled & unscaled)
- Evaluated:
  - Performance metrics
  - Behavioral patterns
  - Sentiment exposure

#### **Visualization**
- Applied PCA (2D reduction)
- Generated scatter plot of trader archetypes

---

## 💡 Key Insights

### 1. Performance Variation by Market Sentiment

| Sentiment | Total PnL | Win Rate | Avg Loss/Trade | Total Loss |
|-----------|-----------|----------|----------------|------------|
| **Greed** | $4.87M | 42.03% | — | -$1.33M |
| **Fear** | $4.10M | — | -$196.35 | — |
| **Neutral** | $1.29M | 39.70% | -$121.73 | — |

**📌 Key Takeaways:**
- **Greed**: Highest opportunity + highest risk
- **Fear**: Skilled traders can profit despite volatility
- **Neutral**: Low-momentum market with minimal activity

---

### 2. Behavioral Adaptation to Sentiment

#### **Trade Frequency**
```
Greed   → 90,295 trades
Fear    → 83,237 trades
Neutral → 37,686 trades
```

#### **Position Sizing**
- **Highest during Fear**: $7,182
- Indicates fewer trades but larger conviction bets

#### **Long/Short Bias**
- Slight **SELL bias** in both Fear & Greed
- **Suggests:**
  - Profit-taking during rallies
  - Defensive positioning in downturns

---

## 👥 Trader Archetypes (7 Clusters)

### Cluster 6: High-Profit, Large-Bet Traders
- **Avg PnL**: $1.87M
- **Avg Trade Size**: $10K
- **Profile**: High-conviction, large position traders

### Cluster 4: High-Activity, Fear-Prone Traders
- **Avg Trades**: 30,688
- **Avg PnL**: $888K
- **Profile**: Strong Fear exposure, high-frequency trading

### Cluster 0: High-Win-Rate, Greed-Oriented Traders
- **Win Rate**: 59.7%
- **Avg PnL**: $259K
- **Profile**: Strong Greed exposure, consistent profitability

### Remaining Clusters
Represent diverse combinations of:
- Win rate variance
- Trade size preferences
- Long/short positioning
- Sentiment-driven strategies

---

## 🎯 Strategy Recommendations

### 1. Dynamic Position Sizing in Fearful Markets

#### **Rule of Thumb**
✅ High-performing traders may increase position sizes on high-conviction trades  
✅ Must combine with strict risk management (tight stop-losses)  
⚠️ Low-PnL traders should remain cautious

#### **Justification**
- High-PnL traders maintain profitability in Fear ($66.38 avg PnL)
- Largest position sizes occur during Fear ($7,182)
- Highest losing-trade loss: -$196.35

---

### 2. Optimized Trading in Greedy Markets

#### **Rule of Thumb**
✅ Increase trading activity during Greed  
✅ Consider profit-taking on longs  
✅ Careful with short positions  
⚠️ Low-profit traders should manage downside risk

#### **Justification**
- Highest trade frequency: 90,295 trades
- Highest total PnL: $4.87M
- Slight SELL bias observed
- Largest total losses: -$1.33M

---








---

**⭐ If you find this project useful, please consider giving it a star!**
