# Project Goal
This was my first dashboard project that I decided to do after exploring PowerBI's features with a practice report. 

# Data Exploration
Reading through the data's dictionary, I can see that the dataset contains tables on payers (insurance providers), patients, encounter information, procedure information, and organization (hospital) information. The encounter and procedure tables are connected through an encounter ID column, and the encounter and patient tables are connected by a patient ID. Many of the cells for the column that either relates to the reason for an encounter or a procedure were left blank, or the reasons were repeated but had different case sensitivity.

# Assumptions
Considering that there were no users to chat with to understand what the purpose of the dashboard should be and the questions that need to be answered, I decided to focus on 3 things: Readmissions, procedures, and payer coverage. This was based on the analysis questions that Maven Analytics had given as part of their challenge for this dataset. 

Things to note:
- A readmission is counted when a patient is readmitted within 30 days of a previous encounter
- Age of the patient is calculated by the age they would be at the end of the year, if a filter on year is selected, or at the time of their death if there is a death date.
- Many of 


# Data Modeling

# Data Transformations

# Data Insights
It should be noted again that this is a synthetic dataset, so any insights gained from this dashboard may not reflect reality.

Based on the dashboard, a few trends can be noted:
- Older patients tend to make up a majority of patients who are readmitted
  - On that note, the dataset seems to skew toward an older population; around 60+ years old
- A significant portion of patients have had a readmittance, which may require further investiation into aftercare treatment
- Those with Medicaid, Medicare, or are Dual Eligible seem to usually have most of their claims cost covered by the payer

# Learning Takeaways
### Do data transformations as upstream as possible.

My main takeaway from creating this dashboard is that I should've done most of the data transformation in SQL. I now understand why many of the data transformations and analysis should be done upstream if possible. However, I wanted to stay in PowerBI to immerse myself in learning the tool, and also understand why doing all of the transformations in PowerBI was a very bad idea, which led to tedious workarounds and long processing times. A lot of my issues would've been solved if I could made columns or done transformation in SQL for the sake of convenience. Plus, I was already familiar with using SQL prior to this project.

### Try to maintain a Star Schema.

From the videos I have seen introducing DAX, the main point that they all shared is that a good data model will reduce the need for complex DAX. The data model in a star schema certainly made doing analysis a lot easier. I believe this was a mistake that I made on my first practice PowerBI attempt, where the data was not following good data model best practices. It was easier to create slicers

