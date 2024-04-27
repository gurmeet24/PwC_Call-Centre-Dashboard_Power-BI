Problem Statement
The purpose of this analysis is to create a dashboard for the call center manager that reflects all relevant Key Performance indicators(KPIs) and metrics in the dataset.

Possible KPIs include(but not limited to):

Overall customer satisfaction
Overall calls answered/abandoned
Calls by time
Average speed of answer
Agents performance quadrant -> average handle time(talk duration) vs calls answered
Data Sourcing
The Dataset used for this analysis was presented by Pwc Switzerland and available at:

Call Center Dataset
Data Preparation
Data transformation was done in Power Query and the dataset was loaded into Microsoft Power BI Desktop for modeling.

The call center dataset is given by a table named:

Call Center which has 10 columns and 5000 rows of observation
The tabulation below shows the Call Center table with its column names and their description:

Column Name	Description
Call Id	Represents every unique observation in the dataset
Agent	Describes the name of the agent
Date	Describes the date of the call
Time	Represents the time of the call
Topic	Describes the topic of the caller
Answered (Y/N)	Describes if the call was Answered or not
Resolved	Describes if the problem was Resolved or not
Speed of answer in seconds	Represents the speed of answer in seconds
AvgTalkDuration	Represents the average talk duration of call
Satisfaction rating	Represents the satisfaction rating of the agent during the call
Data Cleaning for the dataset was done in power query as follows:

Unnecessary columns were removed
Each of the columns in the table were validated to have the correct data type
Unnecessary rows were removed
To ensure the accuracy of the dates in the Date column of Call Center table, a date table was created for referencing using the M-formula:

{Number.From(List.Min(Call Center[Date]))..Number.From(List.Max(Call Center[Date]))}

Here is a breakdown of what the formula does:

For the dataset, we want the start date to reflect the earliest to latest date that we have in the data: January 1, 2021 - March 31, 2021.

The date table was named Calender.

Data Modeling
After the dataset was cleaned and transformed, it was ready to be modeled.

The Calender table was marked as the official date table in the dataset.
A one-to-many (*:1) relationship was created between the Call Center and the Calender tables using the date column in each of the tables

Data Visualization
Data visualization for the datasets was done in Microsoft Power BI Desktop:

The Call Center Manager Page: Shows KPIs including overall customer satisfaction, overall calls answered/abadoned, calls by time, average speed of answer, agents performance quadrant -> average handle time(talk duration) vs calls answered

Data Analysis
Measures used in visualization are:

'#' of answered = Calculate(distinctcount('Call Center'[Call Id]),Filter('Call Center','Call Center'[Answered (Y/N)]="Y"))
'#' of resolved = Calculate(distinctcount('Call Center'[Call Id]),Filter('Call Center','Call Center'[Resolved]="Y"))
Average satisfaction rating = Average('Call Center'[Satisfaction rating])
Average Speed of answer = Average('Call Center'[Average Speed of anser in seconds])
Target Value Satisfaction = 4.5
As shown from Data Visualization, It can be deduced that:

The average satisfation rating is 3.40
81.08% of total calls were answered and 18.92% of total calls were not answered
72.92% of total calls were resolved and 127.08% of total calls were not resolved
Insights
As shown by Data Visualization, It can be deduced that:

In January a total of 1455 calls were answered, whereas 317 calls were not answered
In February a total of 1298 calls were answered, whereas 318 calls were not answered
In March a total of 1301 calls were answered, whereas 311 calls were not answered
The average speed of answer is 67.52 seconds
