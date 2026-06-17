Today I built an AI Vehicle Cost & Fuel Analysis Dashboard using claude :

# 📊 Analysis Findings

### Vehicle Profile

* **Vehicle:** Hyundai Creta 1.5 Petrol
* **Fuel Type:** Petrol
* **Vehicle Age:** 2 Years
* **Monthly Usage:** 1,200 km
* **Dataset:** 52 trip records across 5 fuel types

### Cost Analysis

* Current Petrol operating cost: **₹6.15/km**
* Estimated monthly fuel expenditure: **₹7,385**
* E85 Flex Fuel costs **₹6.37/km**, making it **3.57% more expensive** than Petrol despite its lower pump price.
* The E85 break-even fuel price was calculated at **₹79.11/L**, compared to the actual price of ₹82/L.

### Fuel Type Comparison

| Fuel Type | Cost/km (₹) |
| --------- | ----------- |
| EV        | 1.75        |
| CNG       | 3.32        |
| Diesel    | 4.67        |
| Petrol    | 6.15        |
| E85       | 6.37        |

#### Key Observation

Electric Vehicles (EVs) demonstrated the lowest operating cost, costing nearly **72% less per kilometer than Petrol**.

### Emissions Analysis

CO₂ emissions per kilometer:

| Fuel Type | CO₂ (kg/km) |
| --------- | ----------- |
| E85       | 0.070       |
| EV        | 0.091       |
| CNG       | 0.125       |
| Petrol    | 0.171       |
| Diesel    | 0.179       |

#### Key Observation

* E85 emerged as the cleanest fuel option.
* Diesel generated the highest carbon emissions.
* Petrol ranked among the least environmentally friendly options.

### Vehicle Age Impact

The dashboard revealed that operating costs increase as vehicles age.

| Vehicle Age          | Cost/km |
| -------------------- | ------- |
| New (0–2 years)      | ₹4.23   |
| Mid-Life (3–5 years) | ₹4.09   |
| Aged (6–9 years)     | ₹5.17   |
| Old (10+ years)      | ₹5.29   |

#### Key Observation

Maintenance costs increase significantly for older vehicles, leading to higher total ownership costs.

### Fuel Recommendations

* **Petrol:** Best for daily mixed-use driving where refueling convenience is important.
* **E85:** Best for environmentally conscious drivers prioritizing lower emissions.
* **Diesel:** Suitable for high-distance highway travel.
* **CNG:** Cost-effective for high-mileage urban commuters.
* **EV:** Most economical option for city driving with access to charging infrastructure.

### Dashboard Conclusion

While Petrol remains convenient, the analysis showed that:

* EVs provide the lowest running costs.
* E85 offers the lowest emissions.
* CNG provides an excellent balance between affordability and environmental impact.
* Vehicle age significantly affects total operating expenses.



🎯 Key Learnings

### 1. Prompt Engineering Drives Better Dashboards

Providing detailed requirements helped Claude generate a structured dashboard with KPIs, visualizations, comparisons, and recommendations rather than simple charts.

### 2. AI Can Transform Raw Data into Business Insights

The dashboard not only visualized fuel costs but also derived actionable insights such as break-even fuel prices, monthly expenses, and emission comparisons.

### 3. Comparative Analysis Improves Decision-Making

Comparing Petrol, Diesel, CNG, E85, and EV side-by-side made it easier to evaluate trade-offs between cost, convenience, and sustainability.

### 4. Visualization Enhances Understanding

Bar charts, emission distribution charts, trend lines, scorecards, and comparison cards helped communicate insights more effectively than raw tables.

### 5. Total Cost of Ownership Matters

Fuel price alone does not determine affordability. Maintenance costs, fuel efficiency, vehicle age, and emissions must also be considered.

### 6. Sustainability Can Be Quantified

The dashboard demonstrated how AI can evaluate environmental impact alongside financial metrics, enabling more balanced transportation decisions.

### 7. AI Can Generate Domain-Specific Analytics Applications

This project showed that Claude can be guided to create specialized analytical dashboards for real-world use cases such as fleet management, fuel optimization, and vehicle ownership analysis.

Following are the screenshots of the dashboard provided by claude :
<img width="1920" height="710" alt="Screenshot (263)" src="https://github.com/user-attachments/assets/0cf4eab5-4deb-4062-ad67-5594873d20a6" />
<img width="1920" height="910" alt="Screenshot (262)" src="https://github.com/user-attachments/assets/8177a240-1ead-4069-8a0e-3fb08e649918" />
<img width="1920" height="896" alt="Screenshot (261)" src="https://github.com/user-attachments/assets/fbe9105a-f4af-49c7-a18a-7a6054345346" />


