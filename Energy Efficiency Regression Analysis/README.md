# 🏢 Energy Efficiency: Regression & Machine Learning Analysis

This project explores how **building geometry, glazing, and architectural variables** influence heating and cooling loads using the **UCI Energy Efficiency Dataset**.  
The analysis compares **Linear Regression models** with **Machine Learning models** (Random Forest, Gradient Boosting) to identify:

- Which design features matter most  
- How strongly each variable affects energy use  
- Which predictive model provides the best performance  
- How architects can optimize building energy efficiency early in design  

---

## 📺 Presentation Video

Click below to watch the presentation on YouTube:

[![Watch the presentation on YouTube](https://img.youtube.com/vi/HnM6KpukYFM/0.jpg)](https://www.youtube.com/watch?v=6AwPaPJzARk&t=2s)

**Watch here:** https://youtu.be/HnM6KpukYFM?si=FPzDMK5fnLZj1uAp

--- 

## 📘 Project Overview

Early building design has the largest influence on operational energy use.  
Using the UCI Energy Efficiency dataset, this project quantifies how features such as:

- **Relative Compactness**
- **Surface Area / Wall Area / Roof Area**
- **Height**
- **Glazing Area**
- **Glazing Distribution**
- **Orientation**

affect **Heating Load (Y1)** and **Cooling Load (Y2)**.

The modeling approach includes:

### ✔ Exploratory Data Analysis  
Histograms, scatter plots, correlation matrix, and boxplots reveal strong patterns:

- Compactness → **lower loads**  
- Height → **higher loads**  
- Glazing → **higher loads (nonlinear)**  
- Orientation → **negligible effect**

---

## 📊 Regression Models

### **Linear Regression**  
- Explained ~90% of variance  
- Residual diagnostics revealed **nonlinearity**, **non-normality**, and **heteroscedasticity**  
- Good baseline but **not suitable for accurate prediction**

### **Regularized Models**  
- Ridge/Lasso improve stability  
- Still limited due to nonlinear relationships

---

## 🌲 Machine Learning Models

### **Random Forest**  
- Achieved **near-perfect predictive accuracy (R² ≈ 0.997)**  
- Residuals tightly clustered around zero  
- Captured nonlinear relationships missed by regression

### **Feature Importance**  
Random Forest identifies the major drivers of building energy performance:

1. **Relative Compactness (most important)**
2. **Height**
3. **Roof Area**
4. **Wall Area**
5. **Glazing Area**
6. Orientation (irrelevant)

These align strongly with building physics.

---

## 📈 Actual vs Predicted Performance

Machine Learning models:

- Track true values extremely closely  
- Show consistent performance across low and high loads  
- Dramatically reduce error versus all regression models  

This makes them ideal for **early-stage design analysis**.

---

## 🧠 Key Insights

- **Compact buildings** are significantly more energy efficient.  
- **Taller buildings** require more heating and cooling load.  
- **Glazing >25%** increases energy use sharply without shading.  
- **Orientation** has little measurable impact (in this dataset).  
- **Tree-based ML models** outperform Linear Regression by a large margin.  

---

Daniel Cisneros. (2025). Energy Efficiency: Regression & Machine Learning Analysis.


