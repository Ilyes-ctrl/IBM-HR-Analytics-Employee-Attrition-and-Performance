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

## 3. Is there a relationship between working overtime and leaving the company?
In order to determine whether working overtime is linked to a higher likelihood of leaving the company, I created this visualization with `Overtime` (Yes/No) placed on the
X-axis and a custom DAX measure, `Attrition Yes Count`, mentionned previously on the second question.
### Insights
The results reveal a notable difference: employees working overtime account for 127 attrition cases, compared to 110 cases among those not working overtime. Although the
difference is not overwhelmingly large, the trend suggests that overtime may contribute to higher turnover, possibly due to increased workload, stress, or reduced work-life
balance. For HR decision-making, this insight underlines the importance of monitoring overtime assignments and ensuring proper support mechanisms, as excessive overtime
could be a retention risk factor.

![thirdVisual](/assets/three.png)

*This bar chart represents the relationship between overtime status and employee attrition.*

## 4. Which age groups are more likely to leave, and does gender make a difference?
The goal of this analysis was to identify which age demographics are most vulnerable to attrition and to determine if this trend is uniform across genders. To achieve this,
a calculated measure was engineered to accurately represent the Attrition Rate-the percentage of employees who left within each specific age and gender cohort—rather than
using raw counts. This measure normalizes the data, ensuring a fair comparison between groups of different sizes: 
`Attrition Rate by Gender = 
DIVIDE(
    COUNTROWS(FILTER('IBM HR Analytics Employee Attri', 'IBM HR Analytics Employee Attri'[Attrition] = "Yes")),
    COUNTROWS('IBM HR Analytics Employee Attri')
)`  
The result is visualized in a clustered column chart with `Age` on the x-axis, `Attrition Rate by Gender` on the y-axis, and `Gender` providing the key segmentation.
### Insights
The data reveals a clear and sharp inverse relationship between age and attrition rate, with the youngest employees (ages 18-24) exhibiting a critically high turnover rate
of over 75%. This rate declines precipitously as age increases, effectively plateauing for employees over 40. This indicates that early-career employees are a high-risk
group, likely due to factors like role exploration, lower job satisfaction, or competitive job hopping. Furthermore, the analysis uncovers a significant gender disparity
within these younger cohorts: young women are leaving at a markedly higher rate than their male counterparts. For recruiters and HR business partners, this is a crucial
insight. It suggests that retention strategies—such as enhanced onboarding, career pathing, mentorship programs, and engagement surveys—should be prioritized for employees
under 30, with a particular focus on the experience and needs of young female employees to address this specific gap.

![fourthVisual](/assets/four.png)

*This clustered column chart represents the employee attrition rate across different age brackets, segmented by gender, to identify demographic trends in turnover.*

## 5. Which job roles experience the most attrition, and how do they compare across departments?
This analysis was conducted to pinpoint the specific job roles with the highest turnover and to understand their distribution across the company's primary departments. To ensure an accurate and comparable metric, a DAX measure was crafted to calculate the attrition rate for each job role—the percentage of employees in that role who left the company. This is superior to a simple count of leavers, as it accounts for the total number of employees in each role, preventing larger groups from appearing disproportionately problematic. The measure being: 
`Attrition Rate by Job Role = 
DIVIDE(
    CALCULATE(COUNTROWS('IBM HR Analytics Employee Attri'), 'IBM HR Analytics Employee Attri'[Attrition] = "Yes"),
    CALCULATE(COUNTROWS('IBM HR Analytics Employee Attri'))
)` 
The results are sorted in descending order to immediately highlight the most critical roles, with a color legend applied to segment each bar by its respective department.
### Insights
The data reveals a critical concentration of attrition in individual contributor and highly specialized roles. Sales Representative stands out as the role with the most
severe attrition crisis, with a rate of 40%, significantly higher than all others. This is followed by Laboratory Technician and Human Resources roles. The chart provides
crucial context by department, showing that while Sales is a clear hotspot, Research & Development also faces significant pressure due to the volume of technical roles
experiencing turnover. A key detail to note is the Manager role, which appears twice; this indicates that managers in Sales have a slightly higher attrition rate than those
in R&D, a nuance that would be lost without departmental segmentation. For recruiters and department heads, this analysis moves beyond general department-level data to
identify the exact positions that are retention risks. It suggests a need for targeted interventions, such as reviewing compensation plans for Sales Representatives, career
pathing for Laboratory Technicians, and workload assessments for HR personnel, all tailored to the specific challenges within each department.

![fifthVisual](/assets/five.png)

*This horizontal bar chart represents the attrition rate for each job role within the organization, color-coded by department to contextualize the operational areas most affected.*

# What I learned
- **🔍 Mastering DAX for Accurate Metrics:** I learned to move beyond simple counts and engineer precise DAX measures to calculate normalized rates, such as department and job-role-specific attrition rates. This was critical for ensuring fair comparisons and avoiding misleading conclusions from raw data, solidifying my understanding of how to build accurate and reliable KPIs in Power BI.

- **🎯 The Art of Targeted Analysis:** This project taught me how to drill down from high-level trends (like department attrition) to specific, actionable insights (like the 40% attrition rate for Sales Representatives). I learned the analytical skill of zooming in and out of data to identify not just that a problem exists, but exactly where it is most acute, which is essential for proposing effective solutions.

- **👥 Designing for Contextual Storytelling:** I advanced my visualization skills by learning how to use segmentation and legend encoding effectively. By incorporating fields like Department and Gender into charts, I provided crucial context that transformed a simple bar chart into a multi-layered story, revealing nuances like the differing attrition rates for managers in Sales versus R&D.

- **⚖️ Navigating the Pitfalls of Class Imbalance:** I gained hands-on experience with a classic imbalanced dataset where the majority class (employees who stayed) vastly outweighed the minority (those who left). This taught me the importance of choosing the right metrics (like attrition rate) over default accuracy to build a meaningful analysis that truly captures the phenomenon in question.

# Conclusions

### Insights
1. **👔 Sales and HR Are High-Risk Departments:** The Sales department has the highest attrition rate (21%), closely followed by Human Resources (19%). This indicates that customer-facing and support functions are under significant pressure, potentially from high-stress environments, workload intensity, or a lack of career progression opportunities, directly impacting operational continuity and revenue generation.

2. **🧑‍💻 Early-Career Employees Are the Most Vulnerable:** There is a powerful inverse relationship between age and attrition. Employees in the 18-24 age bracket exhibit a critically high attrition rate of over 75%. This identifies early-career individuals as the highest-risk group, likely due to role exploration, lower initial job satisfaction, or competitive job hopping for better opportunities.

3. **👩‍💼 Retention Strategies Must Be Role-Specific:** Attrition is not uniform within departments. The Sales Representative role is in a crisis with a 40% attrition rate, far exceeding other roles. This pinpoint analysis reveals that blanket department-wide policies are insufficient; interventions must be highly targeted, such as reviewing compensation for Sales Reps and career pathing for Laboratory Technicians.

4. **⚖️ Work-Life Balance is a Key Factor:** Employees who work Overtime show a meaningfully higher count of attrition. This trend suggests a correlation between unsustainable work patterns, burnout, and the decision to leave, highlighting work-life balance as a critical area for HR to monitor and improve through better workload management and support mechanisms.

5. **📈 Normalized Metrics Are Essential for Accurate Analysis:** The highest raw count of attrition came from male employees. However, this primarily reflects the gender distribution of the workforce rather than a higher propensity to leave. This underscores a critical lesson in HR analytics: normalized rates (like attrition rate) are essential for fair comparison and uncovering true insights, preventing misleading conclusions from raw counts.
