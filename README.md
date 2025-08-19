# Overview
 
This project was created to understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.

# The Questions

Below are the questions I want to answer in my project:

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying) 

# Tools I Used

- **Python:** The main tool I used was Python and I also used the following Python libraries:
    - **Pandas Library:** To analyse the data. 
    - **Matplotlib Library:** To visualised the data.
    - **Seaborn Library:** For more advanced visuals. 
- **Jupyter Notebooks:** To run my Python scripts.
- **Visual Studio Code:** For executing Python scripts.
- **Git & GitHub:** For project tracking.

# Data Preparation and Cleanup

## Import & Clean Up Data

```python
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

## Filter US Jobs

The analysis was done for the U.S job market as it had the greatest number of jobs which made it ideal for the project.

```python
df_US = df[df['job_country'] == 'United States']

```

# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

I identified the top 3 most popular data roles, then pulled the top 5 skills for each. This shows the key skills to focus on based on the role I’m targeting.


### Visualise Data

```python
fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```

### Results and Insights:

SQL is the top skill for Data Analysts and Data Scientists, while Python leads for Data Engineers (68%).

Data Engineers need more specialized tools (AWS, Azure, Spark), while Analysts and Scientists focus on broader tools like Excel and Tableau.

Python is highly valued across all three roles, especially for Data Scientists (72%) and Data Engineers (65%).

## 2. How are in-demand skills trending for Data Analysts?

To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

### Visualise Data

```python

from matplotlib.ticker import PercentFormatter

df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

```

### Results and Insights:
- SQL stayed the most in-demand skill year-round, though demand slowly declined.

- Excel demand rose sharply from September, overtaking Python and Tableau by year-end.

- Python and Tableau remained stable with minor fluctuations, while Power BI showed a slight upward trend.

## 3. How well do jobs and skills pay for Data Analysts?

I analyzed U.S. job postings, first looking at salary distributions for common roles (Data Scientist, Data Engineer, Data Analyst) to see which pay the most, then identifying the highest-paying skills and roles by median salary.

#### Visualize Data 

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```

#### Results and Insights

- Salaries vary widely by role, with Senior Data Scientists earning the most—up to $600K—highlighting the value of advanced expertise.

- Senior Data Engineer and Senior Data Scientist roles show many high-end outliers, while Data Analyst salaries are more consistent.

- Median pay rises with seniority and specialization, with senior roles showing both higher averages and greater variation in compensation.

### Highest Paid & Most Demanded Skills for Data Analysts

#### Visualize Data

```python

fig, ax = plt.subplots(2, 1)  

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analystsr')
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()

```

#### Results and Insights:

- Specialized technical skills (e.g., dplyr, Bitbucket, Gitlab) link to higher salaries, sometimes up to $200K.

- Foundational skills (e.g., Excel, PowerPoint, SQL) are most in demand but pay less, showing their importance for employability.

- The gap between high-paying and high-demand skills suggests analysts should build both specialized and core skills to maximize career potential.

## 4. What are the most optimal skills to learn for Data Analysts?

#### Visualize Data

```python
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()

```

#### Results and Insights:

- Oracle commands the highest median salary (~$97K) despite being less common, showing the value of specialized database expertise.

- Widely required skills like Excel and SQL appear often in listings but offer lower median salaries than specialized tools like Python and Tableau.

- Python, Tableau, and SQL Server strike a balance—relatively common and well-paid—making them strong skills for career growth in data analytics.


# What I Learned

In this project, I gained a deeper understanding of the data analyst job market while sharpening my Python skills in data manipulation and visualization. Key takeaways include:

- Advanced Python Skills: Improved proficiency with Pandas for manipulation and Seaborn/Matplotlib for visualizations, enabling more efficient analysis.

- Data Cleaning: Recognized the critical role of thorough cleaning and preparation to ensure accurate insights.

- Skill-Market Alignment: Learned the value of analyzing demand, salaries, and availability to better align skills with career opportunities in tech.

# Insights

This project revealed several key insights about the data analyst job market:

- Skill Demand vs. Salary: Specialized skills like Python and Oracle often command higher salaries, showing a strong link between demand and pay.

- Market Trends: Skill demand shifts over time, making it important for analysts to stay updated to remain competitive.

- Economic Value of Skills: Identifying skills that are both in-demand and well-paid helps prioritize learning for maximum career and financial growth.


# Challenges I Faced

This project posed several challenges but offered valuable learning experiences:

- Data Inconsistencies: Managing missing or inconsistent entries required careful cleaning to maintain analysis accuracy.

- Complex Visualizations: Creating clear and compelling visuals for complex datasets was challenging but essential for effective insights.

- Breadth vs. Depth: Balancing detailed analysis with a broad overview was key to covering the data landscape without losing focus.

# Conclusion

This exploration of the data analyst job market has been highly informative, revealing key skills and trends that shape the field. The insights gained offer actionable guidance for advancing a career in data analytics. As the market evolves, continuous analysis and learning will be essential, making this project a strong foundation for future exploration and growth.


