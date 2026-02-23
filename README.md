# Imperial-Capstone

# Black Box Optimization (BBO) Capstone Project

## 🔍 Non-Technical Explanation
Imagine trying to find the highest peak in a dense, foggy mountain range where you can only take one step per week. You cannot see the landscape; you only know your current altitude after you move. This project solves that problem for eight different mathematical "mountains" (functions) simultaneously.

Instead of guessing blindly, I developed an **Adaptive AI Agent**. It starts like a cautious explorer, mapping the terrain (Exploration). As it gathers data, it behaves like a mountaineer, identifying steep slopes and climbing them aggressively (Exploitation). By the end, it uses a "portfolio" strategy—investing heavily in the most promising peaks while maintaining safety nets for the treacherous ones. The result was a system that transformed 20 limited queries into exponential performance gains.

## 📊 Data
The dataset consists of **160 query-response pairs** collected over 12 weeks.
* **Source:** Generated via a Black Box Optimization oracle as part of the BBO Capstone Challenge.
* **Format:** Continuous input vectors (dimensions 2D to 8D) mapped to scalar objective values.
* **Availability:** The raw query history is available in the `data/` folder of this repository. For full details on the dataset composition and collection, see the [Datasheet](data_sheet.md).

## 🧠 Model
The optimization engine is a **Hybrid Portfolio Strategy** rather than a single static model. It evolved through three phases:
1.  **Bayesian Optimization (Weeks 1-3):** Using Gaussian Processes to map uncertainty.
2.  **Deep Surrogate Modeling (Weeks 4-6):** Using Neural Networks to estimate gradients for rapid ascent.
3.  **Reinforcement Learning Policy (Weeks 7-12):** Treating the optimization as a "Contextual Bandit" problem, dynamically assigning strategies (e.g., "Exploit," "Recover," "Search") to each function based on recent feedback.

For a deep dive into the architecture and trade-offs, see the [Model Card](model_card.md).

## ⚙️ Hyperparameter Optimization
Unlike traditional ML models where hyperparameters are fixed, this project treated **step size** (learning rate) and **exploration radius** as dynamic hyperparameters.
* **Optimization Method:** Manual "Human-in-the-Loop" tuning based on volatility.
* **Strategy:** When a function's performance crashed (e.g., Function 7 in Week 7), the learning rate was decayed. When a gradient was confirmed (e.g., Function 5), the step size was increased to maximize "momentum."

## 📈 Results
The strategy achieved distinct successes across different function landscapes:
* **Exponential Growth:** **Function 5** was the star performer, growing from ~10.0 to **~52.0** by blindly following the neural network's gradient.
* **Recovery:** **Function 7** crashed to 0.42 but was successfully recovered to **>1.0** using a "Backtracking" policy.
* **Breakouts:** **Function 2** stagnated for 8 weeks before a "History Replay" strategy unlocked a new personal best of **0.69**.
* **Visuals:**
![Optimization Landscape Visualization](image.png)
*(Note: This plot illustrates the complexity of the search space, specifically the ruggedness of Function 8 compared to the smoothness of Function 5.)*

## 📬 Contact
* **Author:** Aditya Anggar
* **Email:** ign.aditya.pln@gmail.com
* **LinkedIn/Twitter:** https://www.linkedin.com/in/adityaanggar/
