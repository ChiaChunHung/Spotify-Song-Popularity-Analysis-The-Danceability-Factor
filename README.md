# 🎵 Spotify Song Popularity Analysis: The Danceability Factor
> Exploring the relationship between danceability and song popularity using data from 232,000+ Spotify tracks

## Project Resources

- [📝 Project Brief](./Project_Brief.pdf)
- [📊 Presentation Slides](./Slides.pdf)


## Project Overview

In a music market where **100,000+ songs are uploaded daily** to Spotify, what truly makes a song stand out? This project investigates whether **danceability**—a song's rhythmic suitability for dancing—is associated with higher popularity on Spotify.

Using a comprehensive dataset of 232,726 tracks and multiple linear regression analysis, we explore:
- The relationship between danceability and song popularity
- How other audio features (energy, valence, tempo, acousticness) influence listener engagement
- Genre-specific patterns in music success
- The limitations of predicting popularity from audio features alone

### Research Question

**Do songs with higher danceability achieve higher popularity on Spotify?**

**Hypothesis**: Songs with higher danceability will have higher popularity, controlling for other musical attributes.

---

## Team

**Team C4 - GSBA 545 Final Regression Project**

- **Xiaoyu Ma** - Descriptive Statistics & Visualizations
- **Zhengyuan Pei** - Ideal Experiment Design
- **Hsin-Pan Chen** - Ideal Experiment Design  
- **Dat Nguyen** - Regression Model Development
- **Chia-Chun Hung** - Problem Definition & Regression Results
- **Victoria Nguyen** - Regression Model Development
- **Yang-Hsuan Lin** - Additional Analysis

---

## Dataset

### Source
- **Dataset**: [Spotify Features.csv](https://www.kaggle.com/datasets/somumourya/spotifyfeaturescsv-1)
- **Author**: Somu Mourya (2023)
- **Platform**: Kaggle
- **Size**: 232,726 unique Spotify tracks

### Key Variables

| Variable | Type | Description |
|----------|------|-------------|
| **popularity** | Numeric (0-100) | Track's popularity score (DV) |
| **danceability** | Numeric (0-1) | Suitability for dancing (Main IV) |
| **energy** | Numeric (0-1) | Intensity and activity level |
| **valence** | Numeric (0-1) | Musical positiveness/cheerfulness |
| **tempo** | Numeric | Beats per minute (BPM) |
| **acousticness** | Numeric (0-1) | Acoustic vs. electronic production |
| **loudness** | Numeric (dB) | Overall volume |
| **instrumentalness** | Numeric (0-1) | Likelihood of no vocals |
| **genre** | Categorical | Musical genre classification |

---

## Methodology

### 1. Ideal Experimental Design

To establish causality, we designed an ideal randomized experiment:

**Random Assignment**
- Users randomly assigned to playlists with varying danceability levels (high/low/mixed)
- Balances user preferences and demographic differences

**Standardized Exposure**
- Control for artist popularity, release dates, and algorithmic visibility
- Ensure only danceability varies between conditions

**Confounder Control**
- Hold constant: energy, valence, tempo, acousticness
- Isolate danceability's independent effect

### 2. Statistical Analysis Pipeline

```
Data Collection → Cleaning → EDA → Model Building → Validation → Interpretation
```

**Phase 1: Exploratory Data Analysis**
- Summary statistics calculation
- Distribution analysis (histograms, boxplots)
- Correlation matrix construction
- Visualization of bivariate relationships

**Phase 2: Regression Modeling**
- Multiple linear regression with audio features
- Variable selection based on statistical significance
- Model diagnostics (residual plots, heteroscedasticity checks)
- Robustness testing

**Phase 3: Interpretation**
- Coefficient interpretation with real-world examples
- Prediction interval analysis
- Genre-specific pattern exploration

---

## Key Findings

### Descriptive Statistics

| Variable | Mean | Median | SD | Min | Max |
|----------|------|--------|-----|-----|-----|
| Popularity | 41.13 | 43 | 18.19 | 0 | 100 |
| Danceability | 0.55 | 0.57 | 0.19 | 0.06 | 0.99 |

**Observations**:
- Most songs fall in the **midrange of popularity** (30-60)
- Tracks show **high variation** in listener engagement (SD = 18.19)
- Danceability is **moderately distributed**, with most songs around 0.5-0.6

### Correlation Analysis

| Variable Pair | Correlation (r) |
|---------------|-----------------|
| Danceability ↔ Popularity | **0.26** (positive, modest) |
| Energy ↔ Popularity | 0.25 |
| Valence ↔ Popularity | 0.06 |
| Acousticness ↔ Popularity | **-0.38** (negative) |
| Danceability ↔ Valence | 0.55 |
| Danceability ↔ Energy | 0.33 |

### Final Regression Model

**Model Specification**:
```
Popularity = β₀ + β₁(Danceability) + β₂(Energy) + β₃(Valence) + β₄(Acousticness) + β₅(Loudness) + ε
```

**Results** (N = 232,725):

| Predictor | Coefficient | Std Error | t-value | p-value | Significance |
|-----------|-------------|-----------|---------|---------|--------------|
| **Danceability** | **15.90** | 0.233 | 68.21 | <0.001 | *** |
| Energy | -15.62 | 0.249 | -62.65 | <0.001 | *** |
| Valence | -11.34 | 0.164 | -69.03 | <0.001 | *** |
| Acousticness | -16.19 | 0.144 | -112.51 | <0.001 | *** |
| Loudness | 0.98 | 0.010 | 93.87 | <0.001 | *** |
| Intercept | 61.58 | 0.321 | 191.67 | <0.001 | *** |

**Model Performance**:
- **R² = 0.213** (explains 21.3% of popularity variation)
- **Adjusted R² = 0.213**
- **F-statistic = 10,520** (p < 0.001)

### Key Interpretations

**Danceability has a positive, statistically significant effect on popularity**
- **Effect size**: +15.90 points in popularity per 1-unit increase in danceability
- **Practical interpretation**: A 0.10 increase in danceability → ~1.6 point increase in popularity
- Holding all other variables constant

**Energy, Valence, and Acousticness show negative associations**
- May reflect mainstream preferences for polished, electronic production
- Suggests complexity in listener preferences

**Loudness positively associated with popularity** (+0.98)
- Aligns with modern streaming mastering practices

**Model explains ~21% of variation**
- Reasonable given that popularity depends on non-audio factors:
  - Marketing budgets
  - Playlist placement
  - Artist recognition
  - Social media virality (TikTok trends)
  - Release timing

---

## 🎼 Genre-Specific Patterns

Different genres show varying relationships between danceability and popularity:

| Genre | Danceability-Popularity Pattern |
|-------|--------------------------------|
| **Indie** |  Positive trend |
| **Jazz** |  Positive trend |
| **Soundtrack** |  Slightly negative |
| **Comedy** |  Slightly negative |

**Insight**: Danceability's influence varies by musical context and audience expectations.

---

## Prediction Example

### Test Case: "Submerge" by Movements (Row 12345)

**Track Features**:
```
Danceability: 0.342
Energy: 0.45
Valence: 0.115
Acousticness: 0.0095
Loudness: -8.665 dB
Tempo: 152.308 BPM
Key: C# Major
Time Signature: 3/4
```

**Results**:
- **Actual Popularity**: 42
- **Predicted Popularity**: 50.24
- **95% Prediction Interval**: [18.62, 81.86]

**Analysis**:
- Model slightly overestimates (+8.24 points)
- Wide prediction interval (63 points) reflects high individual variation
- Demonstrates that audio features alone cannot precisely predict single-track success

---

## Limitations & Considerations

### 1. **Observational Data Constraints**
-  Songs aren't randomly assigned → **correlations, not causation**
- Cannot definitively prove danceability *causes* popularity
- Confounding variables may bias estimates

### 2. **Missing Variables**
Factors not captured in the dataset but likely influential:
-  Artist fame and fanbase size
-  Social media virality (TikTok, Instagram Reels)
-  Playlist placement (Spotify editorial picks)
-  Marketing budgets
-  Release timing and trends
-  Use in TV/movies/commercials

### 3. **Platform-Specific Metrics**
- **Spotify's popularity algorithm** is proprietary and opaque
- Scoring may change over time
- Results may not generalize to other platforms (Apple Music, YouTube Music)

### 4. **Model Diagnostics**
- **Heteroscedasticity detected** in residual plots (triangular pattern)
- Variance of errors increases with fitted values
- Suggests potential nonlinear relationships not captured
- Indicates some model assumptions are violated

### 5. **Generalizability**
- Dataset limited to Spotify catalog
- May not reflect preferences on other platforms
- Temporal dynamics not captured (trends change over time)

---

## 💡 Key Takeaways

###  What We Learned

1. **Danceability matters, but isn't everything**
   - Statistically significant positive effect
   - But explains only part of the popularity puzzle

2. **Popularity is multi-dimensional**
   - Energy, valence, tempo, acousticness all play roles
   - Genre context shapes how features influence success

3. **Audio features alone are insufficient**
   - R² of 0.21 shows most variation comes from external factors
   - Marketing, playlisting, and social trends dominate

4. **Genre matters significantly**
   - Danceability's effect varies across musical categories
   - One-size-fits-all strategies may fail

### 📊 Business Implications

**For Artists & Producers**:
- Boosting danceability can help, especially in pop/dance genres
- Don't sacrifice artistic vision solely for metrics
- Consider genre norms when optimizing audio features

**For Music Platforms**:
- Use audio features as part of recommendation algorithms
- But prioritize user engagement signals (plays, saves, shares)
- Recognize that "good music" transcends simple metrics

**For Researchers**:
- Need richer datasets including marketing/promotion data
- Explore nonlinear relationships and interaction effects
- Consider time-series analysis for trend dynamics

## 📚 References & Resources

### Dataset
- **Mourya, S. (2023)**. *Spotify Features CSV*. Kaggle. https://www.kaggle.com/datasets/somumourya/spotifyfeaturescsv-1

### Project Website
- **GitHub Pages**: https://ahsieh53632.github.io/music-attributes-and-popularity/

### Academic Context
- **Course**: GSBA 545 - Regression Analysis
- **Institution**: University of Southern California, Marshall School of Business
- **Semester**: Fall 2025

### Additional Reading
- Spotify API Documentation: https://developer.spotify.com/documentation/web-api/
- Audio Feature Definitions: https://developer.spotify.com/documentation/web-api/reference/get-audio-features

---

## 🙏 Acknowledgments

- **Somu Mourya** for publishing the Spotify Features dataset on Kaggle
- **USC Marshall School of Business** for providing the analytical framework
- **Spotify** for maintaining comprehensive audio feature APIs
- **StatsModels** and **Pandas** development teams for excellent Python libraries

---

## Appendix: Model Diagnostics

### Variance Inflation Factor (VIF)
All VIF values < 5, indicating acceptable multicollinearity levels despite correlations.

### Residual Analysis
- Triangular/funnel pattern indicates heteroscedasticity
- Suggests bounded outcome variable (0-100) creates structural variance
- No extreme outliers detected

### Robustness Checks Conducted
Removed Energy → R² decreased to 0.200  
Removed Loudness → R² decreased to 0.183  
Conclusion: All variables provide unique information
