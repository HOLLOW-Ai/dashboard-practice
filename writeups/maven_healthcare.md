# Project Goal
This was my first dashboard project that I decided to do after exploring PowerBI's features with a practice report. Found a healthcare-related synthetic dataset from Maven Analytics that had a relatively clean dataset. The intended audience is the hospital admins or executives who need insight on the hospital's performance in terms of patient care and costs.


# Data Exploration
Reading through the data's dictionary, I can see that the dataset contains tables on payers (insurance providers), patients, encounter information, procedure information, and organization (hospital) information. The encounter and procedure tables are connected through an encounter ID column, and the encounter and patient tables are connected by a patient ID. Many of the cells for the column that either relates to the reason for an encounter or a procedure were left blank, or the reasons were repeated but had different case sensitivity.


# Assumptions
Considering that there were no users to chat with to understand what the purpose of the dashboard should be and the questions that need to be answered, I decided to focus on 3 things: Readmissions, procedures, and payer coverage. This was based on the analysis questions that Maven Analytics had given as part of their challenge for this dataset. 

Things to note:
- A readmission is counted when a patient is readmitted within 30 days of a previous encounter
- Age of the patient is calculated by the age they would be at the end of the year, if a filter on year is selected, or at the time of their death if there is a death date
- Many cells pertaining to the reason of an encounter or a procedure are empty
- The latest data ends in Feburary 2022, which is seen in the massive dip in the line charts


# Data Modeling
From the start, I thought I would've needed to create 2 fact tables: Encounters and procedures. For every encounter, a patient can have none or multiple procedures which are linked together by an encounter ID in both tables. However, after watching some videos and reading a blog post from the Kimball group, I decided to follow the recommended design structure to model header/line transactions to keep the model in a star schema. It also allows me to turn the reason description column in both tables into its own dimension table. I used a query I found online to create a Date dimension table to make using time-intelligence functions much easier.


# Data Transformations
While transforming columns, this was the main pain point when working entirely in PowerBI. Columns I didn't realize I needed to make would be done in Power Query or created as a calculated column, but at some point it would cause a major slowdown when processing the data. I did create a column to determine the length of stay for each encounter in hours. Knowing the scope of this project, I removed the organizations table that was in the original file since it only contained 1 row of data about the location of the hospital. Additionally, I removed location information from all the tables as my analysis was not focused on geographic analysis.


# Data Insights
It should be noted again that this is a synthetic dataset, so any insights gained from this dashboard may not reflect reality.

Based on the dashboard, a few trends can be noted:
- Older patients tend to make up a majority of patients who are readmitted
  - On that note, the dataset seems to skew toward an older population; around 60+ years old
- A significant portion of patients have had a readmittance, which may require further investiation into aftercare treatment
- Patients with Medicaid, Medicare, or are Dual Eligible seem to usually have most of their claims cost covered by the payer
- Patients with Medicaid have a higher average claim cost
- Pregnancy and heart problems are among the more common reasons for an encounter or a procedure
- Procedure #180325003: Electrical cardioversion makes up a huge bulk of the procedure costs - reason cited is usually atrial fibrillation


# Learning Takeaways
### Do data transformations as upstream as possible.

My main takeaway from creating this dashboard is that I should've done most of the data transformation in SQL. I now understand why many of the data transformations and analysis should be done upstream if possible. However, I wanted to stay in PowerBI to immerse myself in learning the tool, and also understand why doing all of the transformations in PowerBI was a very bad idea, which led to tedious workarounds and long processing times. A lot of my issues would've been solved if I could made columns or done transformation in SQL for the sake of convenience. Plus, I was already familiar with using SQL prior to this project.

### Try to maintain a Star Schema.

From the videos I have seen introducing DAX, the main point that they all shared is that a good data model will reduce the need for complex DAX. The data model in a star schema certainly made doing analysis a lot easier. I believe this was a mistake that I made on my first practice PowerBI attempt, where the data was not following good data model best practices. It was easier to create slicers

### Less is more.

Looking at examples of effective dashboards, there are typicaly a few KPI cards that highlight the most important information for the audience and about 3-4 other visualizations. I learned about the 3-30-300 rule while working on this dashboard, so I opted to retain fewer visualizations instead of having an overwhelming amount of information on one page. If I were to do this project differently, I think I would spend more time on customizing the tooltips so it actually leads to a deeper analysis than keeping the default tooltips as is.


# Final Thoughts

Overall, I am satisfied with the experience I have gained while working on this project. If I were to do things differently, it would be to doing it mostly in SQL and then transition to PowerBI once I've figured out what analysis and insights that I want to showcase. Additionally, I think learning some more DAX functions would be beneficial and having a more solid foundation will help for next time since I spent a good portion of time looking up solutions to questions about a DAX measure I wanted to create or using Copilot to break down what's happening in other users' solutions. Data storytelling is a skill that I do need to work on because it's hard to work on this project in the perspective of someone working as a data analyst because I want to put every visual I can on the page, but the intended user is only going to study the report for maybe a few minutes and only care if the report answers the big questions they have. For the next project, I'm going to try to have the report be 1 page so I can focus on learning what information I need to keep rather than what I want to keep.
