# Kickstarting with Excel

## Overview of Project

### Purpose

Our client is preparing her own Kickstarter campaign to fund her new play. The purpose of this analysis is to discover and track trends among theater focused Kickstarter campaigns. The gathered data will help our client prepare and increase the likelihood of creating a successful campaign.

## Analysis and Challenges

First, I took time to explore the full scope of the Kickstarter data. It includes information on a variety of **types** of Kickstarter campaigns from around the world, the amount of their goals, amount of pledges, number of backers, and the outcome of the campaign. To provide some information at a glance, I used conditional formatting to highlight **successful** versus **failed** campaigns as well as a heat map of the percentage funded.

After a general look at the overall Kickstarter data, I narrowed my focus to the **theater** parent category by separating the **category/subcategory** column using the "Convert Text to Columns Wizard". By doing so, I could generate pivot tables and charts to visualize the data for individual categories and subcategories. In this case, I specifically focused on **theater** and **plays** since our client's campaign falls in this group.

![Category/Subcategory Separation](https://github.com/ChallahBack83/kickstarter-analysis/blob/main/resources/Text_to_Columns.png)


### Analysis of Outcomes Based on Launch Date

Our client wants to know if there is a time of year that will work best to improve the chances of her Kickstarter campaign succeeding. In our Kickstarter data, the dates provided needed to be converted to the standard format. I then used the YEAR() function to create another column containing only the **Year** of the campaign start date. Once this was done, I created a pivot table in a separate sheet that shows the count of each type of outcome per month. Using the **Date Created Conversion** for the rows, the table is organized by month. Adding filters for **Parent Category** and **Years** allows us to isolate the data for a specific year and/or a specific category.

In this case, we care about the **Theater** category. Filtering for **Theater** only and removing information on "Live" campaigns, creates more specific data relevant to our client. I inserted a Pivot Chart to create the following visual.

![Outcomes Based on Launch Date](https://github.com/ChallahBack83/kickstarter-analysis/blob/main/resources/Theater_Outcomes_vs_Launch.png)

The chart suggests that **Theater** campaigns started in May have the highest chance of success while December might not be the best time to launch.

### Analysis of Outcomes Based on Goals

In order to set a realistic campaign goal amount for her Kickstarter, our client needs to understand the rate of success based on the amount of the set goals. After setting up the table below in a separate sheet, we used a COUNTIFS() formula to pull the count of successful, failed, or canceled campaigns for **Plays** based on the given conditions:

    - Goal Amount (i.e. "Less Than 1000")
    - Outcome (Successful, Failed, or Canceled)
    - Subcategory (plays)

![Outcomes_vs_Goals Table](https://github.com/ChallahBack83/kickstarter-analysis/blob/main/resources/Outcomes_Goals_Table.png)

To create this count, we needed to pull information from 3 different columns on the Kickstarter sheet: **D**, **F**, and **R**. On top of that, for most of our categories, **D** (Goal), required two conditions since we were pulling from a range between two numbers.  Most of the formulas looked like:

```
=COUNTIFS(Kickstarter!$D:$D, ">=1000",Kickstarter!$D:$D, "<=4999", Kickstarter!$F:$F, "successful", Kickstarter!$R:$R, "plays")
```
I used $ to create absolutes in order to copy the formulas in the table. I could then edit within the formula and retype less to reduce the chance of errors. Once these counts were gathered, I could generate percentages based on these goals and create the following chart.

![Outcomes_vs_Goals](https://github.com/ChallahBack83/kickstarter-analysis/blob/main/resources/Outcomes_vs_Goals.png)

This chart suggests that campaigns with goals of no more than $4999 are the most likely to be fully funded.

### Challenges and Difficulties Encountered

Being fairly comfortable with Excel, I did not face too many challenges. However, a few things do take a bit to figure out. For instance, when generating the Pivot Table for **"Outcomes Based on Launch Date"**, sorting by months only is not intuitive. When you pull the Date into the Rows, it automatically adds **Quarters**. To get months, you need to remove quarters and it will update the pivot table. I had to play with unchecking boxes until it worked.

Second, the COUNTIFS formula is long and requires a lot of different conditions making it easy to lead to errors in the data. You need to carefully check the formula for typos including every " " and (). For instance, you need to remember to set both sides of the Goal amount with <= and => a. Then, you also need to be certain to add in the subcategory as well, otherwise you'll gather data for the entire sheet. If I didn't know about setting the absolutes to keep my columns for changing when I copied the formula, this too would cause errors. It might lead someone to simply retype the formula for each cell in the table which increases the likelihood of errors.

## Results

- What are two conclusions you can draw about the Outcomes based on Launch Date?

    - Kickstarter campaigns for theater with a Launch Date in May have the most likelihood of being successful.
        -Therefore, if our client launches their Kickstarter in May, it has a better chance of succeeding.
    - The worst time to start a campaign for theater is in December since there is a 50/50 chance it will fail.

- What can you conclude about the Outcomes based on Goals?
    
    - Kickstarter campaigns for plays with goals of no more than $4999 have a higher chance of being fully funded.
        - Therefore, if our client sets a goal of no more than $4999, her campaign has a better chance of succeeding.

- What are some limitations of this dataset?

    - For **"Theater Outcomes by Launch Date"**, we are comparing a count of successful **Theater** campaigns. This category contains everything from building physical theaters to musicals as well as plays. This makes the data less focused so our conclusions may be slightly skewed.
    - We only have data by Country. Since **Theater** is generally an "in person" experience, an understanding of data by City, State, or Region might be helpful. In our modern world, this is not exclusively true, but it would help to see if backers were mostly local to the area where the **Plays** would be performed.
    - Data about campaign backers is also limited only to a count. Besides location, statistics on age, sex, income level, and level of giving across a variety of campaigns could broaden our understanding of the audience and improve marketing.
    - Building upon this, we also do not have data on how backers found and accessed the campaign. Did they find it through an advertisement, social media, word of mouth, or a local event?  Understanding this would allow our client to plan for marketing the Kickstarter.

- What are some other possible tables and/or graphs that we could create?

    - We could create a bar graph to compare the success of campaigns for **Plays** by Country.
    - A graph comparing success rates for campaigns that were put in the **Spotlight** or **Staff Picks** would allow us to gauge the impact on these Kickstarters.

