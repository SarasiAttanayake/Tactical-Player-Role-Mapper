# ⚽ Tactical Player Role Mapper

Unsupervised learning pipeline that discovers tactical player archetypes from World Cup 2026 performance data, then uses those archetypes to build balanced, optimized starting XIs for national teams.

> **Note on data:** This project uses a *simulated* World Cup 2026 player performance dataset, not real match data (the tournament's actual results were not available at the time of dataset creation). The focus here is the methodology — clustering players into tactical roles and optimizing team composition — which applies equally well to real historical tournament data.

---

## Why this project

Football commentary is full of role labels — "the engine," "the destroyer," "the playmaker" — but these are usually assigned by eye, not by data. This project asks: **can tactical roles emerge naturally from performance statistics alone, without any labels?** And once they do, can that structure be used to build a genuinely balanced team rather than just picking the 11 highest-rated players?

## What it does

1. **Cleans and deduplicates** match-level player data into one row per player, aggregating stats sensibly (means for per-match performance, max for tournament totals).
2. **Selects and standardizes** 20 performance features spanning attacking, defensive, and physical output.
3. **Reduces dimensionality with PCA**, retaining components that explain 85% of variance, to stabilize the clustering step against correlated features.
4. **Clusters players with K-Means**, choosing the number of clusters via silhouette score rather than a fixed guess.
5. **Names each cluster** based on its most distinctive statistical strengths (e.g. high distance covered → "The Engine," high tackle rate → "The Destroyer").
6. **Builds optimized starting XIs** with a custom `OptimalTeamBuilder` that balances individual quality, positional requirements, and role diversity — avoiding a team that's all one archetype (the "too many cooks" problem).
7. **Visualizes results** on a rendered pitch, showing each player's position, role, and stats at a glance.

## Key insights

- The optimal number of tactical archetypes, chosen via silhouette score, was 4.
- The most common archetype across the dataset was the Defender.
- Balanced-strategy team optimization consistently outperformed pure quality-first selection on role diversity while sacrificing minimal average rating.



## Example output

```
![Team pitch visualization](images/Visualization.jpg)
```

## Tech stack

- **Data processing:** pandas, numpy
- **Modeling:** scikit-learn (StandardScaler, PCA, KMeans, silhouette_score)
- **Visualization:** matplotlib, seaborn (custom pitch-rendering functions)

## How to run

1. Clone this repo:
   ```bash
   git clone https://github.com/yourusername/tactical-player-role-mapper.git
   cd tactical-player-role-mapper
   ```
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn
   ```
3. Download the dataset from [Kaggle: FIFA World Cup 2026 Player Performance Dataset](https://www.kaggle.com/datasets/rauffauzanrambe/fifa-world-cup-2026-player-performance-dataset) and place the CSV in a `data/` folder.
4. Open and run `tactical-player-role-mapper.ipynb` top to bottom.

## Project structure

```
tactical-player-role-mapper/
├── tactical-player-role-mapper.ipynb   # Main analysis notebook
├── README.md
└── data/                                # (not included — download from Kaggle)
```

## Possible extensions

- Validate archetype stability across seasons/tournaments rather than a single dataset
- Compare K-Means against Gaussian Mixture Models for soft (probabilistic) role assignment
- Extend the team builder to a true genetic algorithm with crossover/mutation instead of weighted random sampling

## Author

**Sarasi Attanayake** — [LinkedIn](https://www.linkedin.com/in/sarasiattanayake/)
MSc Data Science, Statistics and Decision Analysis, Stockholm University
