## Link to YouTube presentation: https://youtu.be/LJAeP8igfI0
# Future Footprints: Predicting Trends in Greenhouse Gas Emissions
![ppt title page](https://github.com/user-attachments/assets/1fb4b6b5-5e25-44a2-9dd6-282ea94a4a6a)

Climate change is a pressing and fundamental crisis, primarily driven by human emissions of CO₂ and other greenhouse gases. In this practicum project, I aim to dig deeper into this issue by explicitly identifying the key factors contributing to increased emissions and forecasting how emission rates will likely evolve in the coming years. Additionally, since effectively reducing emissions requires an understanding of their sources, this project will focus on determining the primary contributors to greenhouse gas emissions and predicting future emission trends.

### Background
Greenhouse gases (GHGs), including carbon dioxide (CO₂), methane (CH₄), nitrous oxide (N₂O), water vapor, and synthetic fluorinated gases, play a critical role in Earth's climate system. These gases naturally trap some of the sun's heat, helping maintain a stable climate suitable for life. However, human activities have significantly increased their concentrations in the atmosphere. 

For instance, the National Oceanic and Atmospheric Administration (NOAA) Global Monitoring Laboratory reported that atmospheric CO₂ levels reached approximately 430 parts per million (ppm) in early 2025, a significant rise from pre-industrial levels of around 280 ppm. Similarly, methane concentrations have increased dramatically, with current atmospheric levels above 1,900 parts per billion (ppb), more than double the pre-industrial levels.
![NOAA graph](https://github.com/user-attachments/assets/fe859d11-a998-4e75-92c1-b569865a76c8)

These increased greenhouse gas concentrations amplify the natural greenhouse effect, resulting in global warming and significant shifts in climate patterns. The consequences include extreme weather events, rising sea levels, disruptions to ecosystems, and adverse health effects. Addressing the increase in greenhouse gases is crucial for environmental sustainability, economic stability, and human health. 

### Project Overview
This project applies unsupervised learning techniques to explore and analyze greenhouse gas emissions data, aiming to reveal hidden patterns and insights without predefined labels. Furthermore, the analysis  utilizes Principal Component Analysis (PCA) to simplify complex, multi-dimensional emissions data into easily interpretable visual forms. Additionally, the project aims to identify countries or sectors that exhibit unusual emission patterns. Ultimately, the project illustrates emission trends across various countries through data visualization, highlighting distinct clusters of countries sharing similar emission profiles, economic activities, or sustainability practices.

### Project Timeline
The project timeline is divided into eight weekly phases, providing a roadmap from initial setup to final presentation. 
![project timeline](https://github.com/user-attachments/assets/8902dc38-044f-4022-8c99-ba5543f86c0d)

### Dataset Overview
#### Basic information:<br/>
- Rows: 44,079 <br/>
- Columns: 22<br/>
#### Key columns include:<br/>
- Sector metrics: Year, incorporated_country, Primary activity, Primary sector<br/>
- Financial metrics: Market_Cap_USD, Revenue_USD, netIncome_USD, etc.<br/>
- Emission metrics: Scope_3_emissions_amount, Scope_3_emissions_type, country_ghg_avg<br/>
- Country statistics: country_population_avg, country_gdp_avg

### Exploratory Data Analysis
EDA is conducted to investigate and understand the relationships among greenhouse gas emissions, country-specific statistics, and financial metrics. It examines data patterns, trends, and correlations to know how these factors interact.

#### Emission Trends Over Time
This chart illustrates the average annual emissions. The sharp decrease from 2020 to 2021 was primarily due to the global lockdowns resulting from the COVID-19 pandemic. Since then, the upward pattern could reflect economic recovery or growth in high-emission sectors.

![linechart](https://github.com/user-attachments/assets/5aa3e822-45f9-4ecd-b5b3-f8991cc3d269)

#### Distribution of Scope 3 Emissions
The distribution of Scope 3 emissions is highly right-skewed, indicating that most entities report relatively lower emission amounts, while a smaller number of entities have significantly higher emissions. A log-scale transformation clearly reveals the skewness and helps visualize the data spread effectively, highlighting the presence of outliers or extreme values. The presence of high-emission outliers suggests that certain countries or companies disproportionately contribute to total emissions.

![emissiondistribution](https://github.com/user-attachments/assets/6ad8a01c-792c-49b1-81c2-fea63b041f4b)

#### Scope 3 Emissions by Primary Sector
Looking at the Scope 3 emissions by primary sector boxplots, clear variations exist among sectors regarding their emissions profiles. Some sectors display significantly higher median emissions and a broader range, indicating that emissions are strongly sector-dependent. Therefore, sector type is a strong determinant of emission levels.

![boxplots](https://github.com/user-attachments/assets/abb3b26f-cbdf-45c7-91a3-6e91b347e5c5)

#### Emissions by Sector over Time 
The plot identifies a sector with the highest average emission rate over time. Looking back at the original dataset before preprocessing, sector 34 is oil & gas processing (refineries). The trends highlight how sector-specific strategies may be needed to curb emissions effectively.

![emissionsbysector](https://github.com/user-attachments/assets/bbe27ebb-cbc9-4935-84c3-a181df924357)

#### Correlation Matrix (All variables)
The heatmap identifies smaller sections of strong correlations between financial metrics and emissions. Variables with no inherent ordering or meaningful distance for clustering will be dropped from the analysis. A smaller heatmap will be used to show correlations specifically between financial metrics and emissions.

![heatmap_allvariables](https://github.com/user-attachments/assets/6a3c06c2-92d9-4ca8-b7ab-a4705dafddb3)

#### Correlation Matrix (Financial Metrics & Emissions)
This smaller heatmap illustrates relationships among greenhouse gas emissions, country statistics, and financial metrics. Financial metrics have strong positive correlations and are strongly interrelated. Emissions (Scope_3_emissions_amount) have notably weak correlations with most financial metrics, suggesting other factors might influence emissions. The country_ghg_avg variable strongly correlates with both country_population_avg and country_gdp_avg. That could indicate some relationship that could be explained with further analysis.

![correlationwithfinancialmetrics](https://github.com/user-attachments/assets/855547e8-c46b-4f64-8c2a-8c674952c68c)

### Clustering Analysis & Dimensionality Reduction (PCA)
The Elbow Method was applied to choose the optimal number of clusters (k=9). Clustering analysis has been performed to find groups of countries or companies based on their emissions. Appropriate features were selected because they directly relate to greenhouse gas emissions and help explain emission patterns. Using categorical codes that don’t have a clear order or meaningful distance would add noise to the model. The PCA projection reduces the 10-feature dataset into two principal components (PC1 and PC2), capturing the most variance for clear visualization. 
![kmeansclustering9_model 1](https://github.com/user-attachments/assets/fefaafaa-4cd3-4c78-aa8e-78f23f455208)

Although the elbow method indicates that the dataset has nine optimal clusters, we will use the silhouette score to verify this number. Based on the result, 2 clusters and 11 clusters performed the best. I will rerun the model with k=2 and k=11 values and gather the predictions. And to confirm, I will also visualize them in a PCA plot.
![kmeansclustering2_model 2](https://github.com/user-attachments/assets/741329df-c8e3-48fd-b8ae-9359be4cfeef)  ![kmeansclustering11_model 3](https://github.com/user-attachments/assets/b5b7c12b-765e-4df5-8a32-1f82d9737cae)

### Findings & Results
At this point, the silhouette score and the PCA plot of the model both show that the clustering of 11 (k=11) yields the best results. A scatter plot will be used to visualize the results of a K-Means clustering analysis, specifically showing how data points are clustered based on their Sector ID after applying PCA (dimensionality reduction).
![clusteringwithsectorid](https://github.com/user-attachments/assets/bd7c68d6-5fef-4e58-8da8-48d4b7022b3d)

- #### Interpretation of K-Means clustering result colored by Sector ID   
  Colors in the plot denote different Sector IDs, effectively illustrating how entities from various sectors are distributed across clusters. Every cluster has a diverse mix of sectors, rather than one   
  cluster being dominated by a single industry. This diversity implies that the clustering is influenced by a combination of factors, such as market capitalization, revenue, Scope 3 emissions, GDP, and 
  population, rather than just industry type.

- #### Overlapping Sectors 
  Some sectors appear across multiple clusters, showing that emissions behavior varies even within a single industry. For example, entities within the same sector may differ in their emissions behavior depending 
  on their geographical and economic context. 

- #### Outliers
  A few points are positioned far from the center of cluster formations, suggesting they are outliers or unique profiles. These might be countries or companies with extreme Scope 3 emissions, exceptionally high 
  or low market cap, or unique sector behavior.

- #### Conclusion 
  In conclusion, this diversity implies that clustering is influenced by a combination of factors rather than industry type alone. The plot reveals that complex interplays of sectoral, economic, and national 
  characteristics shape emission behavior. Additional analysis is required to gain more insight. Ultimately, the unsupervised learning approach effectively illustrates multi-dimensional patterns beyond simple 
  categorical grouping.

### Future Steps
It would be valuable to identify which sectors dominate each cluster by cross-tabulating Cluster versus Sector ID, gaining insights into which industries contribute the most to each emission behavior group. This can support targeted policy-making and sustainability strategies tailored to the emission profiles of different clusters.

### References
Global Monitoring Laboratory. (2025). Trends in Atmospheric Carbon Dioxide. NOAA. Retrieved from https://gml.noaa.gov/ccgg/trends/

Global Monitoring Laboratory. (2018). Summary Report No. 29 2014 - 2018. NOAA. Retrieved from https://gml.noaa.gov/publications/summary_reports/summary_report_29.pdf 












