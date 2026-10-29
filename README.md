# SaaS Ticket Support Dashboard

An end-to-end analytics project built with MySQL and Power BI to transform synthetic SaaS support ticket data into an interactive dashboard to support operational monitoring and business decision-making.

This project covers the BI workflow from data preparation, data modeling, dashboard development and business recommendations.

## About the Project
A SaaS ticketing system is a cloud-based software tool that support requests related to application performance, authentication, integrations, billing, and other technical issues. As ticket volumes grow, it becomes increasingly important to monitor support operations and understand recurring issues.

In this project, I built an analytics solution using a synthetic dataset of 100,000 SaaS support tickets generated between 2022 and 2025.

The project focuses on analyzing support ticket volume, resolution time, ticket status, customer satisfaction, reopened tickets and issue types to identify potential areas for operational and process improvement purpose.

The analysis combines SQL-based data preparation with Power BI dashboard development and business-oriented recommendations.

## Business Questions
This project focuses on answering the following business questions:
1. How does support ticket volume change over time?
2. How are tickets distributed across statuses, priorities, and customer segments?
3. Which product areas and issue types generate the most support tickets?
4. How do resolution time, customer satisfaction, and reopening rates vary across product areas and issue types?

## Dataset
Source: [Synthetic IT / SaaS Support Tickets Dataset](https://www.kaggle.com/datasets/ahsanneural/synthetic-it-support-tickets/data)

Data Volume: 100,000 tickets

Period: 2022–2025

Each row represents a support ticket generated for a fictional SaaS platform. The dataset contains structured ticket information and customer support details without using real customer data.

Key fields include:
- Ticket ID
- Created At
- Customer ID
- Customer Segment
- Channel
- Product Area
- Issue Type
- Priority
- Status
- SLA Plan
- Initial Message
- Agent First Reply
- Resolution Summary
- Resolution Time Hours
- Reopened
- Customer Sentiment
- CSAT Score
- Has Attachment
- Platform
- Region

  
## Project Workflow
The project follows an end-to-end analytics workflow:
1. Import raw ticket data into MySQL Workbench.
2. Prepare and clean the data using SQL.
3. Build the required data model and establish key relationships.
4. Import the prepared data into Power BI.
5. Perform additional transformations using Power Query.
6. Develop DAX measures and interactive dashboards.
7. Identify potential business improvement opportunities based on the analysis.


## Data Preparation
The raw dataset was imported into MySQL Workbench for initial data preparation before being used in Power BI.

The main tasks included:
- Inspecting the structure and consistency of the raw dataset.
- Creating staging tables for raw and cleaned ticket data.
- Standardizing data types and preparing fields for analysis.
- Checking ticket identifiers and data consistency.
- Creating an issue dimension using Product Area and Issue Type.
- Generating an Issue Key to link issue categories with the fact table.
- Validating issue key matching before removing redundant columns from the fact table.

Additional transformations were performed in Power Query, including:
- Converting the ticket creation timestamp into separate date and time fields.
- Removing unnecessary text fields from the analytical fact table.
- Preparing the data model for reporting and DAX calculations.
- Handling missing CSAT values so that unavailable ratings are not treated as valid scores.

These steps prepared the dataset for consistent analysis and dashboard development.

## Data Model
The project uses a structured data model to support ticket analysis and reporting.

The model includes:
- Fact Tickets: Stores ticket-level information and analytical measures.
- Dim Issue: Organizes Product Area and Issue Type into a dimension linked to the fact table through an Issue Key.
The data model was designed to reduce redundant issue-category information and support analysis across product areas and issue types.

<img width="1167" height="678" alt="image" src="https://github.com/user-attachments/assets/1e02ed1f-8b7a-4b71-9c07-e480a1cdc30c" />

## Dashboard
The Power BI report is divided into two pages, each focusing on a different aspect of support operations.
The dashboard screenshots can be filtered to 2025 for presentation purposes, while the underlying dataset covers 2022–2025.

### 1. Support Operations Overview
<img width="1122" height="622" alt="image" src="https://github.com/user-attachments/assets/dee40859-2831-49ec-8b5d-8c9d2364fb1d" />

The first page provides an overview of support operations through key performance indicators and ticket distribution analysis.

Key metrics and visualizations include:
- Total Tickets
- Average Resolution Time
- Active Tickets
- Average CSAT Score
- Ticket Reopened Rate
- Monthly Ticket Volume Trend
- Tickets by Status
- Tickets by Priority
- Tickets by Customer Segment
- Tickets by Region

This page helps users monitor overall support demand, ticket status, and customer experience.

### 2. Issue Analysis
<img width="1118" height="626" alt="image" src="https://github.com/user-attachments/assets/d3201adb-c879-46a2-a273-e28733f814b4" />

The second page focuses on ticket distribution and operational performance across product areas and issue types.

Key metrics and visualizations include:
- Tickets by Product Area
- Ticket Volume by Issue Type
- Reopened Rate by Issue Type
- Average Resolution Time by Issue Type
- Average CSAT by Issue Type
- Product Area Performance Matrix

This page helps users compare issue categories and identify areas that may require further investigation or process improvement.

## DAX Measures
Key measures developed for the dashboard include:
- Total Ticket Count
- Average Resolution Time
- Average CSAT Score
- Active Ticket Count
- Reopened Ticket Count
- Ticket Reopened Rate

These measures support the analysis of support demand, resolution efficiency, and customer experience.

## Key Insights & Business Recommendations
The dashboard provides an overview of support operations, while further analysis helps translate the observed patterns into potential business improvement opportunities.

The following hypotheses were developed from the synthetic dataset. They are intended to guide operational review and further investigation rather than establish confirmed root causes.

### 1. Outstanding Tickets: Maintaining an Efficient Support Workflow

#### What the Data Shows
In 2025, the dataset contains 25,162 support tickets, of which 10,107 (40.2%) are classified as Open, In Progress, or On Hold. The average resolution time for tickets with a recorded resolution time is approximately 44.93 hours.

To understand whether this pattern was unique to 2025, I also examined data from earlier years. The distribution of ticket statuses remained broadly similar, while ticket volumes across Product Areas were relatively evenly distributed.

#### Business Insight
The historical comparison does not indicate an obvious new imbalance in ticket status or a sudden concentration of demand within one Product Area. Instead, outstanding tickets appear to be a recurring part of the support operation.

However, a consistent ticket distribution does not necessarily mean that every case is progressing efficiently. The 40.2% outstanding-ticket share provides a useful starting point for examining whether unresolved cases receive appropriate follow-up and are progressing within reasonable timeframes.

This distinction matters because tickets in progress or on hold are not automatically overdue. Without information about how long individual tickets have remained in each status, the current figures cannot establish that a serious backlog exists.

#### Business Hypothesis
The support team may benefit from more systematic monitoring of outstanding tickets to maintain an efficient workflow and ensure timely follow-up.

#### Business Recommendations
1. **Introduce ticket aging monitoring.** Categorize outstanding tickets by time since creation and highlight cases that remain unresolved beyond internally defined thresholds.
2. **Establish regular backlog reviews.** Review older Open, In Progress, and On Hold tickets to determine whether they require follow-up, escalation, additional information, or reassignment.
3. **Monitor operational trends over time.** Track outstanding-ticket volume, ticket status distribution, and average resolution time to identify meaningful changes in support demand or resolution performance.

Business Objective: In order to maintain an efficient support workflow, improving the visibility of outstanding cases and identify tickets that may require additional attention before delays become significant.

### 2. Mobile App: Reviewing the Handling of Security-Related Tickets

#### What the Data Shows
In 2025, the Mobile App's Security Concern issue type recorded a reopened rate of 7.49%, an average resolution time of 44.89 hours, and an average CSAT score of 2.81/5.

To better understand the nature of these tickets, I reviewed the initial messages and resolution summaries. A common initial message was *There seems to be a vulnerability in the mobile app functionality.* Hence, the resolution summaries frequently described actions such as investigating logs, mitigating the issue and updating security settings.

The major tickets are marked as Resolved in the dataset indicating that they reached a resolved status. However, the combination of a 7.49% reopened rate and a relatively low CSAT score highlights an opportunity to examine how reported security concerns are handled and whether the resolution process can be improved.

#### Business Insight
The ticket descriptions suggest that users have reported concerns about potential vulnerabilities in the Mobile App while the resolution summaries describe actions such as log investigation, mitigatio and security-setting updates.

Despite these recorded actions, the issue category has a reopened rate of 7.49% and an average CSAT score of 2.81/5. These results provide a reason to examine how security-related tickets are assessed, resolved, and followed up after closure.

Reopened tickets does not necessarily mean that the original fix failed. It may reflect a recurring issue, additional information from the customer or a further investigation requirement. Similarly, the initial message indicates a reported concern, not definitive proof that an actual security vulnerability was confirmed.

The key business question is therefore not simply whether these tickets were marked as Resolved, but whether the handling process consistently addresses reported concerns and provides an appropriate resolution experience.

#### Business Hypothesis
Mobile App security-related tickets may benefit from a more structured investigation, resolution verification, and follow-up process to reduce recurring cases and improve customer experience.

#### Business Recommendations
**1. Standardize the handling of reported security concerns.** Define clear procedures for assessing, documenting and escalating suspected vulnerabilities to the appropriate technical or security team.
**2. Strengthen resolution verification.** Establish suitable checks to confirm that the required investigation and corrective actions have been completed before closing a ticket.
**3. Review reopened cases.** Examine reasons of security-related tickets are reopened and identify whether recurring problems, incomplete fixes or communication gaps that require further attention.
**4. Monitor resolution outcomes.** Track reopened rate, resolution time and CSAT to evaluate whether changes to the handling process improve the customer support experience.

Business Objective: Improve the consistency of security-related ticket handling, identify opportunities to reduce recurring cases, and strengthen customer confidence in the support process.

Important limitation: This analysis is based on synthetic data. The findings identify potential areas for investigation but do not establish that the fictional organization has a confirmed security vulnerability or a proven process failure.

## Repository Structure
The repository may be organized as follows, depending on the files included in the final project:

```
IT-Support-Ticket-Analytics
│
├── Dataset
│   └── synthetic_it_support_tickets.csv
│
├── MySQL
│   ├── Data Cleaning.sql
│   ├── Data Preparation.sql
│
├── Power BI
│   ├── IT Support Ticket Analytics.pbix
│
│
└── README.md
```

## Tools & Technologies
| Tool | Purpose |
|------|---------|
| MySQL Workbench	| SQL-based data preparation and data modeling |
| SQL	| Data cleaning, validation, and transformation |
| Power BI |	Dashboard development and interactive reporting |
| Power Query |	Data transformation and preparation |
| DAX |	KPI calculations and analytical measures |
| Dimensional Modeling |	Structuring data for analytical reporting |
| GitHub |	Version control and portfolio presentation |

## Skills Demonstrated 
- SQL
- Data Cleaning and Validation
- Data Preparation and ETL
- Data Modeling
- Dimensional Modeling
- Power Query
- DAX
- Power BI Dashboard Development
- KPI Development
- Operational Performance Analysis
- Business Insight Development
- Hypothesis-Driven Analysis
- Business Recommendations
