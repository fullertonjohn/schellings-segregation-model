# Schelling's Model of Segregation — Interactive Simulation

An independent project implementing Thomas Schelling's classic model of residential segregation from scratch in Python, exploring how a simple neighbor-similarity preference produces large-scale segregation patterns. The finished deliverable is an interactive Streamlit simulation.

## Status

This project is no longer under active development. It started with a broader goal — modeling inter-party neighbor tolerance among voter blocs and analyzing the resulting data in STATA — which was not carried through. What was completed, and is the project's output, is the interactive simulation (`interactive.py`) and the exploratory notebooks and example dataset behind it.

## Try it

```
pip install streamlit numpy
streamlit run interactive.py
```

The app displays a 100×100 grid of two "parties" (blue/red) plus empty cells. Sidebar controls let you set the relocation threshold (how large a fraction of different-party neighbors an agent will tolerate before moving) and toggle a highway barrier splitting the grid. "Run Simulation" steps the model until no agent is unhappy; "New Random Grid" reseeds it.

## How the model works

- Agents sit on a grid; each has up to 8 neighbors (Moore neighborhood).
- An agent is *unhappy* if the fraction of its neighbors belonging to the other party exceeds the relocation threshold.
- Each iteration, every unhappy agent moves to a random empty cell; this repeats until no unhappy agents remain (equilibrium).
- Segregation is measured with a mean similarity score: the average, across agents, of the fraction of same-party neighbors.
- An optional "highway" — two impassable columns down the middle of the grid — can be added to see how a physical barrier affects the outcome.

## Repository contents

- **`interactive.py`** — the Streamlit app; the final deliverable. Core simulation logic (the model above) is original; the Streamlit UI scaffolding was generated with LLM assistance (noted in the file header).
- **`schelling-model.ipynb`** — the original single-run notebook: builds a random grid, runs the simulation once with and once without a highway, and visualizes the before/after grid states.
- **`schelling-model-repeated.ipynb`** — a batch-run notebook: repeats the simulation 100 times for each of several relocation thresholds (tolerances of 2, 3, 4, and 5 out of 8 neighbors), with and without a highway, recording each run's final similarity score to `schelling_simulation_output.csv`.
- **`schelling_simulation_output.csv`** — example batch-run output. Columns are the final mean similarity score and a highway flag (0 = no highway, 1 = with highway); the tolerance level used for each run isn't retained in this file.

## Running the notebooks

Requires `pandas`, `numpy`, and `matplotlib`.
