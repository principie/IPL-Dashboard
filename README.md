# IPL-DASHBOARD


## Problem Statement

- Find the Title Winner, Orange Cap Winner, Purple Cap Winner, Tournamnet 6's and 4's for the respective season on IPL.
- Develope IPL Batting and Bowling stats and add a filter where user can select the bowler and batter to see these stats.
- Winning perecntage based on the toss decision.
- Matches win by venue.
- Total wins by team in a season.
- Matches won based on the result type.


### STAKEHOLDERS
- BCCI
- Franchise/ Team Owners
- Team management
- Coaches
- Players
- Media 
- Public

### FUNCTIONALITIES
- Data modeling with three tables
- Data cleaning in Power Query
- Time Intelligence function 
- Creating KPI's 
- Dax Queries
- Creating and formating charts
- Different DAX functions like Calculate,Sum,Sumx,Filter,Allselected,
  values,selectedvalue,return,concatenate,diving etc
- Creating different shapes and formating
- Generating insights from charts
- Export report

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : **Data Processing** -> Create Calender Table 
           
            Calender Table = CALENDAR(MIN(ipl_matches_2008_2022[match_date]),MAX(ipl_matches_2008_2022[match_date]))

- Step 3 : For extract the year from this date table created new column (Year)

            Year = YEAR('Calender Table'[Date])
   This particular table will be used as a filter which will be representing a season.
- Step 4 : **Data modeling** -> Create a relationship between those tables and create a column named Date.
        ![Screenshot 2024-04-10 194037](https://github.com/principie/IPL-Dashboard/assets/93659513/71863c62-f580-4232-8029-da96c01d21d5)
        You can see a relationship has been created over here which represents one to many.
- Step 5 :  Then select Slicer for season and place the `Calender[Year]` table into the field section and change the slicer style into dropdown. 
- Step 6 : Write a DAX funtion to determine the select season or Title Winner. Created a new measure in 'ipl_matches_2008_2022' table. To find the title winner we have to find max date. **In every season the last match played was final match and who won that particular match was title winner.**

           
           Title Winnner = VAR max_date = CALCULATE(MAX('Calender Table'[Date]),ALLSELECTED(ipl_matches_2008_2022), VALUES(ipl_matches_2008_2022))
           var title_winner = CALCULATE(SELECTEDVALUE(ipl_matches_2008_2022[winning_team]), 'Calender Table'[Date] = max_date)
           return title_winner
A card visual was used to represent the **Title Winner**.

![Screenshot 2024-04-10 215155](https://github.com/principie/IPL-Dashboard/assets/93659513/63313b72-436f-4011-a5f6-1c658a846aca)
- Step 7 : Select a card and choose 'ipl_ball_by_ball_2008_2022' table, then drag the 'batter' into filter section and **choose top N**, then take sum of batter-run and put it into by values. Then select another card and **choose sum of batsman-run to get total runs he made**. To join two particular fields used `CONCATENATE` function. And it also represents the **Orange Cap Winner**. Same for **Purple Cup Winner**.
           
           Batter Runs = CONCATENATE(SUM(ipl_ball_by_ball_2008_2022[batsman_run]), " Runs")
           Bowler Wickets = CONCATENATE(SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery]), " Wickets")




     ![Screenshot 2024-04-10 220333](https://github.com/principie/IPL-Dashboard/assets/93659513/6721da1e-c023-4d48-a53f-3fabbc5f412c)
- Step 8 : For the 6's & 4's choose `∑ batsman-run`and in basic filtering section choose only 6 and same for 4's.

     ![Screenshot 2024-04-10 225652](https://github.com/principie/IPL-Dashboard/assets/93659513/4472533f-9600-4439-955b-2c511829471d)
     
