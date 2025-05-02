

# Robust Malware Defense for Android

## 📌 Project Overview

This project tackles the pressing issue of malware detection on Android platforms using advanced machine learning and reinforcement learning techniques. We explore the TUANDROMD dataset, which comprises 4465 Android apps represented by 241 features (permission-based and API-based), and design a system to accurately classify apps as **malware** or **goodware**.


## 🧠 Problem Definition

Traditional signature-based malware detection methods struggle with novel or polymorphic threats. Our objective is to develop a **robust and efficient machine learning pipeline** to detect Android malware, with an emphasis on adversarial robustness and high accuracy.

## 🛠️ Methodology

### 1. Data Preprocessing

* Cleaned dataset and removed underrepresented classes
* Label encoded targets
* Standardized features using `StandardScaler`
* Balanced data using **SMOTE**

### 2. Feature Engineering

* Divided features into:

  * Permission-based (1–214)
  * API-based (215–241)
  * Combined

### 3. Model Training

* Models used:

  * Random Forest
  * SVM
  * Logistic Regression
* Hyperparameters optimized via cross-validation

### 4. Evaluation

* Metrics: Accuracy, Precision, Recall, F1-score
* Stratified train/test splits
* Confusion matrix heatmaps with `seaborn`

### 5. Adversarial Training

* Built a custom `AdversarialEnv` using OpenAI Gym
* Used **Proximal Policy Optimization (PPO)** from `stable-baselines3`
* Generated adversarial examples and retrained models with perturbed data

### 6. Feature-Based Analysis

* Evaluated model performance on different feature types separately

---

## 📊 Results

### Clean Data Accuracy

| Feature Set      | Random Forest | SVM | Logistic Regression |
| ---------------- | ------------- | --- | ------------------- |
| Combined         | **93%**       | 87% | 86%                 |
| Permission-based | 89%           | 84% | 81%                 |
| API-based        | 85%           | 81% | 82%                 |

### Adversarial Accuracy

| Feature Set      | Random Forest | SVM | Logistic Regression |
| ---------------- | ------------- | --- | ------------------- |
| Combined         | 73%           | 72% | 72%                 |
| Permission-based | 73%           | 70% | 67%                 |
| API-based        | 70%           | 67% | 68%                 |

### FGSM/PGD/CW Attacks (ε = 0.1)

* Accuracy dropped \~20% with adversarial examples
* Most effective attack: CW (85% accuracy)

---

## ⚠️ Challenges

* High computational cost (especially for PPO and adversarial training)
* Designing realistic RL environments
* Stability of RL training
* Generalizing to unseen malware strains

---

## ✅ Conclusion

By combining **Random Forests** with **Deep Q-Networks**, this project demonstrates an effective hybrid defense strategy for Android malware detection. The model shows promise under adversarial conditions, though further improvements in robustness are necessary for real-world deployment.

