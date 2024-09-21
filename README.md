# The Analysis

## 1. What skills are most in demand for the top 3 popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on my target role. 

View my notebook with detailed steps here: [2_Skills_Count.ipynb](DA_project/2_Skills_Count.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)
sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == job_title].head(5)
    bar_plot = sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 80)
    
    # Add value labels on each bar
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.1f}%', va='center')
    
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])


fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=16)
plt.tight_layout()
plt.show()

```

### Results

![Visualization for Top Skills](images/skills_percentage.png)

### Insights

- Python is a versatile skill that is highly demanded across all three roles, but it is most prominent among data scientists (72%) and data engineers (68%).

- SQL is the most requested skill for data analysts and data engineers, and it is used in over half the job postings for data analysts and over 68% for data engineers. Python is the most sought-after skill for data scientists, appearing in 72% of job postings.

- Data Engineers require the most specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists, who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).