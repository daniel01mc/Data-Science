# **Paper Helicopter Experiment (Last Experiment)** 
---
#### **Daniel Cisneros - Experimental Design** 
---
## **Walkthrough and Findings:**
For this experiment we have **22 Files** from different students with unique type of paper helicopters **dropped at different heights to measure flight time** with the following designs:

- **WingLength**: 6.5 cm,  8 cm, 9.5 cm
- **BodyLength:** 6.5 cm, 8 cm, 9.5 cm
- **BodyWidth:** 4 cm, 5 cm, 6 cm
- **PaperClip:** y, n
- **Tape:** y, n

**Steps:**
1. **Reading and Cleaning Files**
2. **Combining Files**
3. **Explore Combined Data**
4. **Data Insights and Viz**
5. **Create Models**
    - **Regression Model 1 and Random Forest**
        - Observations (interaction, Box-Behnken, Visualizations) and Summary
    - **Regression Model 2 and Random Forest**
        - Observations (interaction, Box-Behnken, Visualizations) and Summary
6. **Summary and Optimal Helicopter**


Files had outliers, written mistakes, missing columns, missing headers, and additional information. 
After combining the files, additional changes needed to be done such as one-hot-encoding for categorical values, additional outliers, additional unique parameters, duplicates.
There were some extreme outliers specially on the data collected at 3.0 meters which seems unreasonable which one can conclude that the experiment was not collected appropiatly or there were some extreme conditions. 
Model 1 had an $R^2$ = 77.9% which is slightly lower to Model 2 with a $R^2$ = 78.7% with both having high adjusted R-squared. Based on these results which includes linear, quadratic, and interaction terms. One can say that the drop height is one of the dominant key terms but there seems to be an optimal height for our helicopter. Having very short or very long wings benefits the design but not a mid-range wings creating like U-shape, long wings are more effective at higher drops. Longer bodies also seem to increase flight time and longer bodies at higher drops increases fligh time. It also seems that wider bodies at higher drops increase the time. All these factors can be affected by different conditions such as being more stable, air resistance, center of mass.
The combinations to avoid are having very long wings with body long bodies at the same time. Of course, low heights will reduce the time. Also having mid range wings seems not optimal for any case. 
