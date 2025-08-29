# Introduction
Employee attrition is a major challenge for organizations as it increases recruitment costs, reduces productivity, and impacts overall performance 👥.
To better understand the factors driving attrition, I analyzed the IBM HR Analytics Employee Attrition & Performance dataset 📊 from Kaggle, which contains detailed information
on employees’ demographics, job roles, income, satisfaction levels, and work patterns. Using Power BI ⚡, I cleaned and transformed the data, created key KPIs,
and built interactive dashboards 📈 that highlight attrition trends across departments, genders, age groups, job roles, and overtime status, providing actionable insights
to support HR decision-making.
🔗 Want to explore the project?
- **📊 Dashboard Preview (PDF):** [ibmhr.pdf](ibmhr.pdf)
- **📑 Dataset (Excel):** [ibmhr.xlsx](ibmhr.xlsx)
- **🛠️ Power BI Template (PBIT):** [ibmhr.pbit](ibmhr.pbit)
# Background
### The Questions I Wanted to Answer Through This Project Were:
1. Which departments have the highest employee attrition?
2. Does gender play a role in employee attrition?
3. Is there a relationship between working overtime and leaving the company?
4. Which age groups are more likely to leave, and does gender make a difference?
5. Which job roles experience the most attrition, and how do they compare across departments?
# Tools I Used
- **📂 Kaggle:** Source of the IBM HR Analytics Employee Attrition & Performance dataset
- **📝 Excel:** Initial data exploration and cleaning
- **⚡ Power BI:** Data transformation, KPI creation, and interactive dashboard design
- **💻 GitHub:** Documentation and sharing the project
# The Analysis
The dashboard visualizations were built to address key questions about employee attrition and performance. Each chart was designed to highlight a specific factor influencing
turnover, from demographics to job roles and departments. But how exactly did I go about answering these questions?
## 1. Which departments have the highest employee attrition?
In order to figure out which departments have the highest employee attrition, I created this visualization using the `Department` field on the Y-axis and a calculated measure
of `Attrition Rate` on the X-axis. The measure was defined as: `Attrition Rate = DIVIDE([Employees Left], [Total Employees], 0)`. This approach was chosen because it
provides a normalized percentage rate, allowing a fair comparison across departments of different sizes. Using just the `Attrition` column would only show counts of
employees who left, which can be misleading when departments have unequal headcounts. The legend was also set to `Department` to ensure each category is clearly
distinguished.
### Insights
The results show that Sales has the highest attrition rate (21%), followed by Human Resources (19%), while Research & Development records the lowest attrition at 14%. These
findings suggest that Sales and HR are more vulnerable to turnover, possibly due to workload intensity, stress, or limited career growth opportunities. Meanwhile, R&D
demonstrates relatively stronger employee retention, indicating higher stability and satisfaction levels. For the company, the high attrition in Sales is especially critical
as it can directly impact revenue generation and client relationships, making it a priority area for targeted retention strategies.

![firstVisual](/assets/one.png)

*This bar chart represents employee attrition rates across different departments.*

## 2. Does gender play a role in employee attrition?
In order to figure out whether gender plays a role in employee attrition, I created this donut chart with `Gender` in the legend and a DAX measure for `Attrition Yes Count` in the values: `Attrition Yes Count = CALCULATE(
    COUNTROWS('IBM HR Analytics Employee Attri'),
    'IBM HR Analytics Employee Attri'[Attrition] = "Yes")` 
I chose this measure instead of using the raw `Attrition` column because it allows me to filter and count only the employees who actually left, providing a clear breakdown
of attrition numbers per gender. This way, the chart directly shows the proportion of leavers rather than including employees who stayed, making the visualization more
targeted and easier to interpret.
### Insights
The results show that 150 male employees left (63.29%) compared to 87 female employees (36.71%). While this indicates that a larger share of attrition cases comes from men,
it’s important to note that this chart reflects absolute counts of attrition, not normalized attrition rates by gender. Since the company has more male employees overall,
this difference may simply reflect workforce distribution rather than a higher likelihood of men leaving. The key takeaway is that attrition affects both genders
significantly, and gender alone is not the strongest explanatory factor — other aspects such as department, overtime, and age may offer more actionable insights.

![secondVisual](/assets/two.png)

*This donut chart represents the distribution of employees who left the company, segmented by gender.*
