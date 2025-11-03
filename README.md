# GreenMetrics-Dashboard
End-to-End Project: From Data Cleaning in Python to Interactive Insights in Power BI  Analyzing ESG, CO₂, and GDP data to assess environmental sustainability and industrial impact.

🚀 Project Overview

This project integrates Python (for data preparation & EDA) and Power BI (for visualization) to analyze how industries perform in terms of sustainability, carbon emissions, and economic efficiency.

It brings together ESG (Environmental, Social, Governance) metrics, CO₂ data, and GDP indicators to reveal how economic progress aligns—or conflicts—with environmental responsibility.

🧩 Workflow Summary
Step	Stage	Tools Used	Description

1️⃣	Data Loading	Python (pandas)	Loaded ESG and CO₂ datasets

2️⃣	Data Cleaning	Python	Handled missing values, standardized columns, removed duplicates

3️⃣	Data Merging	Python	Merged ESG and CO₂ data on common keys (like Country/Industry/Year)

4️⃣	Exploratory Data Analysis (EDA)	Python, Seaborn, Matplotlib, Plotly	Visualized distributions, trends, and correlations

5️⃣	Dashboard Creation	Power BI	Designed a professional ESG × CO₂ insight dashboard

6️⃣	Insight Generation	Power BI, Python	Derived key findings on sustainability efficiency and emission intensity

🧹 1. Data Preparation in Python

✅ Steps Performed:

Loaded both ESG dataset and CO₂ dataset using pandas

Cleaned column names and removed nulls

Filtered relevant columns (Industry, Year, ESG_Score, CO2_Emissions, GDP, Population)

Created derived metrics:

CO2_per_Capita

Green_Efficiency_Index = ESG_Score / CO2_Emissions

Merged datasets into one unified DataFrame for further analysis.

📊 2. Exploratory Data Analysis (EDA)

Performed extensive EDA to uncover sustainability insights and correlations between ESG, CO₂, and GDP metrics.

🔍 EDA Visuals & Insights

Distribution of ESG Scores – Understanding overall score distribution across companies

Distribution of ESG Grades – Visualized proportions of AAA–BBB ratings

Average ESG Score by Industry – Identified sustainability leaders

Average CO₂ Emission by Industry – Highlighted high-polluting sectors

ESG Score vs CO₂ Emission – Checked inverse relation between ESG & carbon output

Correlation Heatmap – Explored relationships among ESG, CO₂, GDP, and Population

Top 1 Greenest Company – Displayed top performer by ESG score

Yearly CO₂ and GHG Trend – Time-series view of emissions and GHG over years

🧠 Code Highlights

# Top 1 Greenest Company
top_green = merged.sort_values('ESG_Score', ascending=False).head(1)

plt.figure(figsize=(10,6))

sns.barplot(x='ESG_Score', y='Company', data=top_green, palette='Greens')

plt.title('Top Greenest Company by ESG Score', fontsize=16, weight='bold')

plt.tight_layout()

plt.show()

# Yearly CO₂ and GHG Trend

yearly = merged.groupby('Year')[['CO2_Emissions', 'CO2_per_Capita', 'Total_GHG']].mean().reset_index()

fig = px.line(

    yearly,
    
    x='Year',
    
    y=['CO2_Emissions', 'Total_GHG', 'CO2_per_Capita'],
    
    title='Yearly CO₂ and GHG Trend - United States',
    
    markers=True
    
)

fig.show()


✅ Insight Gained:

Some industries with higher GDP still emit significantly more CO₂ per capita.

CO₂ and GHG emissions have shown mixed trends — improvements in some sectors, stagnation in others.

ESG and CO₂ show a strong negative correlation (better ESG → lower emissions).

💡 3. Power BI Dashboard Design

🎨 Dashboard Features

Page 1: Executive Overview (KPIs + Key Trends)

Average ESG Score, CO₂ Emission, CO₂ per Capita

Treemap of CO₂ Emission Breakdown by Industry

Donut Chart of ESG Grades

Line Chart for ESG Trends (2010–2020)

Text Insight: “Sustainability Snapshot”

Page 2: Industry Comparison

ESG vs CO₂ (Clustered Column)

Green Efficiency Index Map

Gauge Chart for Sustainability Balance

Top & Bottom ESG Industries Cards

Interactive Filters: Industry, Year, Country

⚙️ 4. Key DAX Measures

AvgESG = AVERAGE('Data'[ESG_Score])

AvgCO2 = AVERAGE('Data'[CO2_Emissions])

CO2_per_Capita = DIVIDE(SUM('Data'[CO2_Emissions]), SUM('Data'[Population]))

Green_Efficiency_Index = DIVIDE(AVERAGE('Data'[ESG_Score]), AVERAGE('Data'[CO2_Emissions]))

Highest ESG Industry = 

VAR _TopIndustry =

    TOPN(
    
        1,
        
        SUMMARIZE(
        
            'merged_esg_co2_clean',
            
            'merged_esg_co2_clean'[Industry],
            
            "AvgESG", AVERAGE('merged_esg_co2_clean'[ESG_Score])
            
        ),
        
        [AvgESG],
        
        DESC
        
    )
    
RETURN

    MAXX(_TopIndustry, 'merged_esg_co2_clean'[Industry])

Lowest ESG Industry = 

VAR _BottomIndustry =

    TOPN(
    
        1,
        
        SUMMARIZE(
        
            'merged_esg_co2_clean',
            
            'merged_esg_co2_clean'[Industry],
            
            "AvgESG", AVERAGE('merged_esg_co2_clean'[ESG_Score])
            
        ),
        
        [AvgESG],
        
        ASC
        
    )
    
RETURN

    MAXX(_BottomIndustry, 'merged_esg_co2_clean'[Industry])

    Carbon_Impact_Index = 
    
DIVIDE(AVERAGE('merged_esg_co2_clean'[CO2_Emissions]), AVERAGE('merged_esg_co2_clean'[GDP])) * 1000


    
📈 5. Insights Derived

🌱 ESG leaders tend to have significantly lower CO₂ emissions

💰 High GDP ≠ High ESG — some economically strong sectors still underperform environmentally

🌍 The Green Efficiency Index effectively identifies sectors balancing economy & ecology

📉 Gradual improvement in CO₂ and GHG trends, but per capita emission remains high

🧭 Industry-level analysis highlights actionable sustainability gaps

🎯 6. Future Scope

Integrate real-time ESG & emission APIs

Predict ESG trends using Machine Learning (Regression or LSTM)

Add country-level dashboards for global benchmarking

Develop RAG (Risk–Assessment–Governance) scoring automation

👩‍💻 7. Tools & Technologies

Category	Tools Used

Data Handling	Python, Pandas, NumPy

Visualization	Matplotlib, Seaborn, Plotly, Power BI

Modeling (optional)	Scikit-learn

Dashboard Design	Power BI Desktop

Dataset	ESG and CO₂ datasets (2010–2020)

🏁 8. Conclusion

This project bridges the gap between economic performance and environmental responsibility.

By merging data analytics with visualization, it helps identify industries that are truly sustainable — and those that need urgent reform.

The dashboard serves as a data-driven sustainability compass, enabling organizations to track progress, compare industries, and plan greener strategies for the future.

👤 Author

Smriti Pandey

B.Tech – CSE (AIML) | Data Analyst 

📍 GTBIT, New Delhi
