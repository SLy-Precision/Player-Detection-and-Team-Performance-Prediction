# Player Detection and Team Performance Prediction (AEGIS Engine)

This project is a complete framework to identify talented players using advanced metrics and then predict their potential performance when integrated into a new team. The core of this framework is the **AEGIS (Adaptive Ensemble Game Insight Simulator)**, a proprietary engine that simulates soccer matches to provide data-driven insights for player recruitment.

## 🚀 Project Goal

The primary goal of this project is to reduce the uncertainty and financial risk associated with player transfers in professional soccer. By simulating a player's performance within a new team's tactical context, we can answer the pivotal question: *"How would this player actually perform on our team?"*

## ⚙️ Core Component: The AEGIS Engine

AEGIS is a simulation engine that conceptualizes a soccer match as a sequence of discrete events. It uses a cascaded ensemble of six specialized **XGBoost models** to predict the outcome of each event in sequence. The output of one model becomes the input for the next, creating a rich, context-aware prediction pipeline.

The engine deconstructs each event into several predictable facets:
1.  **Event Type:** What is the next action? (e.g., Pass, Shot, Dribble)
2.  **Event Accuracy:** Will the action be successful?
3.  **Goal Outcome:** If the action is a shot, will it be a goal?
4.  **X Coordinate:** Where on the pitch (length) will the next event occur?
5.  **Y Coordinate:** Where on the pitch (width) will the next event occur?
6.  **Time Delta:** How much time will elapse until the next event?

This architecture allows for the generation of realistic, dynamic match simulations from which performance metrics can be derived.

## 📂 Project Pipeline & Methodology

The project is structured across several notebooks, each handling a specific part of the pipeline.

###  notebooks

#### 📋 `00_Data_Analysis_Extraction_Evaluation_.ipynb`
* **Objective:** Data sourcing, cleaning, and initial exploratory data analysis (EDA).
* **Process:** Extracts granular event data from Statsbomb for thousands of Liga MX matches. Performs initial cleaning and visual analysis to understand the data's structure and distributions.

#### 📈 `01_Modeling_Using_Data_&_Creation_of_Advanced_Statistics_.ipynb`
* **Objective:** Feature engineering and the creation of advanced performance metrics.
* **Process:** Develops and calculates Key Performance Indicators (KPIs) to evaluate players beyond traditional stats. This forms the basis for the talent identification phase.

#### 🎯 `02_Detection_of_Talent.ipynb`
* **Objective:** Identify "hidden gems" and high-potential players using the advanced metrics developed previously.
* **Process:** Applies the KPIs to the player database to rank and filter players, identifying transfer targets that traditional scouting might overlook.

#### 🤖 `03_AEGIS.ipynb`
* **Objective:** Build, train, and validate the base AEGIS simulation engine.
* **Process:**
    1.  Prepares the historical event data by creating a "context window" (using the 5 previous events to predict the next one).
    2.  Trains the six-model XGBoost cascade on the full dataset of Liga MX matches.
    3.  Validates the base engine by simulating matches and comparing the statistical distribution of simulated events to real-world data, ensuring the engine produces realistic outcomes.

#### 🔬 `04_AEGIS_Simulations.ipynb`
* **Objective:** Apply the AEGIS engine to a real-world use case: projecting the impact of a new player at a specific club.
* **Process:**
    1.  **Fine-Tuning:** The base AEGIS models are fine-tuned on a "hybrid" dataset. For example, to test Player X at Club América, a new dataset is created containing Club América's data with the outgoing player's events removed and Player X's events inserted.
    2.  **Simulation:** The newly fine-tuned models are used to simulate a full season (or a large number of matches).
    3.  **Analysis:** Key performance metrics from the simulation (e.g., Expected Goals For/Against, Win Percentage) are compared against the team's real-world performance to provide a quantitative measure of the player's potential impact.

## 🛠️ Key Technologies
* **Data Manipulation & Analysis:** Pandas, NumPy
* **Machine Learning:** Scikit-learn, XGBoost
* **Data Visualization:** Matplotlib, Seaborn, Mplsoccer
* **Data Sourcing:** Statsbomb API

## ▶️ How to Use
To replicate this project, run the Jupyter notebooks in numerical order:
1.  Start with `00_Data_Analysis...` to process the raw data.
2.  Run the `01_...` notebooks to generate advanced statistics.
3.  Use `02_Detection_of_Talent` to identify potential players.
4.  Execute `03_AEGIS` to train the base simulation engine.
5.  Finally, use `04_AEGIS_Simulations` to fine-tune the models for a specific player and run performance projections.

*Note: Training the base models in `03_AEGIS` can be computationally intensive and may take a significant amount of time.*

## 🚀 Future Work
* **Expand Datasets:** Incorporate data from other leagues (e.g., Premier League, La Liga) to create more robust and transferable models.
* **Team-Style Fine-Tuning:** Fine-tune the AEGIS engine on data from specific teams to capture their unique tactical styles more accurately.
* **Alternative Architectures:** Explore the use of neural network architectures (like LSTMs or Transformers) as an alternative to the XGBoost ensemble, comparing performance and execution time.
