# ⚡ Public EV Charging Access in New Jersey: Spatial Statistics Analysis

This project examines how **public electric vehicle (EV) charging infrastructure** is distributed across **New Jersey census tracts**.  
The analysis uses spatial data, demographic variables, maps, Moran’s I, and count regression models to understand whether public EV charging access is:

- Evenly distributed across neighborhoods  
- Concentrated in specific counties or corridors  
- Associated with socioeconomic tract characteristics  
- Spatially clustered rather than randomly located  
- Influenced by geographic factors not fully captured by demographics  

---

## 📺 Presentation Video

Add your presentation video link here:

[![Watch the presentation on YouTube](https://img.youtube.com/vi/6AwPaPJzARk/0.jpg)](https://www.youtube.com/watch?v=6AwPaPJzARk&t=2s)

**Watch here:** https://www.youtube.com/watch?v=6AwPaPJzARk&t=2s

---

## 📘 Project Overview

Public EV charging access is important for the transition to cleaner transportation.  
While New Jersey has a growing EV charging network, access depends not only on the number of chargers statewide, but also on **where chargers are located**.

This project asks:

> Are public EV charging stations evenly distributed across New Jersey census tracts, or are they concentrated in certain socioeconomic and geographic areas?

The unit of analysis is the **census tract**, which provides a neighborhood-scale view of infrastructure access.

---

## 🗂️ Data Sources

The analysis combines three main datasets:

### **Public EV Charging Station Data**
- Public open EV charging station locations
- Latitude and longitude coordinates
- Level 2 port counts
- DC fast charging port counts
- Charging network and station attributes

### **ACS Demographic Data**
- Total population
- Median household income
- Poverty rate
- Households without vehicle access
- Owner-occupied housing share

### **Census Tract Boundaries**
- New Jersey tract polygons
- GEOID identifiers for joining data
- Land area for density calculations
- Geometry for mapping and spatial joins

---

## 🧹 Data Cleaning and Spatial Join

The workflow includes:

### ✔ ACS Cleaning
- Converted ACS variables from text to numeric values
- Recoded Census missing-value sentinels to `NA`
- Calculated poverty, no-vehicle, and owner-occupancy rates only when denominators were valid

### ✔ EV Station Filtering
Stations were filtered to keep only:

- New Jersey stations
- Public access stations
- Open stations
- Stations with valid coordinates

### ✔ Spatial Join
EV charging stations are point locations, while ACS data are tract-level polygons.  
To connect them, station points were spatially joined to the census tract that contains them.

Both layers were projected to **EPSG:5070** before spatial operations.

---

## 📊 Statewide Charging Snapshot

The filtered dataset includes:

- **2,181** New Jersey census tracts
- **1,822** public open EV charging stations
- **3,965** Level 2 ports
- **2,062** DC fast ports
- **6,027** total charging ports
- **701** tracts with at least one public station
- **1,480** tracts with no public station
- **32.1%** of tracts contain at least one public EV charging station

This shows that public charging infrastructure exists statewide, but is concentrated in a minority of tracts.

---

## 🗺️ Exploratory Spatial Analysis

### **County-Level Concentration**
The counties with the most public stations are:

1. **Bergen**
2. **Middlesex**
3. **Essex**
4. **Hudson**
5. **Morris**

County totals provide a useful first look, but they are raw counts and do not adjust for population or neighborhood-scale variation.

### **Zero-Heavy Station Counts**
The station count distribution is strongly zero-heavy:

- Most tracts have **zero** public EV stations
- A smaller number of tracts contain several stations
- A few tracts act as high-count infrastructure hubs

This supports using a **count model** rather than ordinary linear regression.

### **Stations per 10,000 Residents**
The main population-adjusted access measure is:

```text
stations per 10k = (station count / population) × 10,000
```

Very low-population tracts can create unstable per-capita rates, so tracts with population below 500 were excluded from rate-based views.  
Map values were capped at 75 for display only.

---

## 🧭 Accessibility and Context Maps

The project includes several maps to compare different dimensions of access:

### **Charging Availability Map**
Shows cleaned stations per 10,000 residents by tract.

### **Median Household Income Map**
Provides socioeconomic context for where charging access appears higher or lower.

### **No-Vehicle Household Map**
Shows areas where transportation access may already be limited.

### **Distance to Nearest Charger Map**
Measures distance from each tract representative point to the nearest public charger.

This distance map is important because a tract can have zero stations inside its boundary but still be close to a charger in a neighboring tract.

---

## 🌐 Spatial Autocorrelation

### **Global Moran’s I**
Moran’s I tests whether nearby tracts tend to have similar charging access.

The cleaned station-rate Moran’s I result is:

- **Moran’s I = 0.0907**
- **p-value = 1.754 × 10⁻¹³**

This indicates **modest but statistically significant spatial clustering**.

In plain language: public EV charging access is not randomly scattered across New Jersey. Nearby tracts tend to have somewhat similar levels of access.

---

## 📈 Regression Modeling

### **Why Negative Binomial Regression?**

Station counts are:

- Nonnegative integers
- Zero-heavy
- Right-skewed
- Overdispersed

Because of this, a **negative binomial regression model** is more appropriate than ordinary linear regression.

The model includes:

- Median household income
- Poverty rate
- No-vehicle household share
- Owner-occupied housing share
- Population density in the refined model
- `log(Population)` as an offset

The population offset allows the model to compare station availability relative to tract population size.

---

## 🔍 Baseline Model Results

The baseline model shows:

- **Median income** is positively associated with public station counts
- **Owner-occupancy** is negatively associated with public station counts
- **Poverty rate** is not a strong predictor
- **No-vehicle household share** is not a strong predictor in the baseline model

A $10,000 increase in median household income is associated with about a **3.8% higher expected station count**, holding other variables and population constant.

---

## 🏙️ Density-Adjusted Model

A second model adds population density as a geographic control.

The density-adjusted model improves fit:

- Baseline AIC: **about 5030**
- Density-adjusted AIC: **4950.9**

Lower AIC indicates better model fit.

However, the density coefficient should be interpreted carefully because the model already includes population as an offset.  
The negative density result may suggest that some charging stations are located in commercial, highway, workplace, parking, or destination-oriented tracts rather than the most densely residential tracts.

---

## 🧩 Residual Analysis

Residual maps show where the model predicts too many or too few stations:

- **Red tracts** have more stations than predicted
- **Blue tracts** have fewer stations than predicted
- Residual clustering remains statistically significant

Residual Moran’s I:

- **Residual Moran’s I = 0.0952**
- **p-value = 1.523 × 10⁻¹⁴**

This means the model still misses important geographic structure.

Likely omitted factors include:

- Highway and interchange access
- Commercial land use
- Parking availability
- Retail and employment centers
- Tourism and destination charging
- Utility and grid capacity
- EV ownership and adoption rates

---

## 🧠 Key Insights

- Public EV charging access in New Jersey is **uneven**.
- Only about **one-third of census tracts** contain a public EV charging station.
- Station counts are **zero-heavy and right-skewed**.
- Charging access is **modestly but significantly spatially clustered**.
- Higher-income tracts are associated with more public charging stations.
- Owner-occupied tracts are associated with fewer public stations.
- Demographics explain part of the pattern, but **geography and land use remain important**.
- Future work should include highway access, commercial land use, employment centers, parking, EV adoption, and network travel time.

---

## ⚠️ Limitations

This project is exploratory and should not be interpreted as causal.

The analysis identifies spatial patterns and statistical associations, but it does not prove that income, housing patterns, or other demographic variables cause charger placement.

The analysis also uses census tracts, but actual charging access can cross tract boundaries.  
The distance-to-nearest-charger measure helps address this, but network travel time would provide a better accessibility measure.

---

## ✅ Conclusion

Public EV charging infrastructure in New Jersey is spatially uneven and clustered.  
Although the state has more than 1,800 public open EV charging stations and over 6,000 ports, only about one-third of census tracts contain at least one public station.

The results suggest that EV charging access is not just a technology issue.  
It is also a **spatial planning and equity issue**.

---

Daniel Cisneros. (2026). *Public EV Charging Access in New Jersey: Spatial Statistics Analysis*.
