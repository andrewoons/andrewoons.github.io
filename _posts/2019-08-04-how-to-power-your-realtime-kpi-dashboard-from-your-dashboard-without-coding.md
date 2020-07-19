---
layout: post
title: 'How to power your reailtime KPI dashboard from your database without coding'
date: 2019-08-04 11:33:00 +0100
categories: how-to
---

<img src="https://miro.medium.com/max/700/0*_bLpu-FW0aFkKe1I.png" />

Realtime insight into your business metrics is key to making the right decisions. KPI dashboards showing your most important metrics are a powerful tool.

However, setting up a dashboard, getting the right data and automating it so that the information is always live, usually means asking a developer to build something.

Especially when you want to see different time-periods, compare things or want to add a new metric, you have to go back to a developer and wait hours if not days.

Luckily, there is a solution! The combination of Trevor, Google Sheets and Geckoboard allows you to add new metrics powered directly by your database, updating in realtime, without needing a developer.

We are using this internally and it’s pretty sweet. Adding new metrics now takes us a couple of minutes. All you need is three tools and some Excel magic.

So let’s get right into it — in our example we will be adding a KPI showing our sales numbers. We want to show the data in multiple forms:

- Last 7 days
- Last 30 days
- Quarter to date

## Using Trevor to pull reports from your database

[Trevor.io](https://trevor.io) is a tool that allows you to visually query information from your database. It has quite a powerful visual query editor, so you don’t need any programming knowledge to use it. You can connect most popular databases to it, including Postgres, MySQL, MongoDB and Amazon Redshift.

Once you’ve connected your database, the next thing is to pull a report. In the Query Builder, on the left hand side you can see all of your tables.

<img src="https://miro.medium.com/max/700/1*9azzrHfkHba6yE827KKX1A.png" />

What you usually want is to aggregate numbers per day. We don’t want to pull a report for just the 7 days, 30 days and quarter to date, because that doesn’t give us enough flexibility. It is much better to pull a report that shows you everything on a per day basis, and then use Google Sheets to calculate the right numbers. More on that later, let’s get a report happening first.

<img src="https://miro.medium.com/max/700/1*bwNzswoj6vSWfVZYWdW81w.png" />

The calculate button has two options we are going to use, the “sum” option which sums up different numbers, and the “group by” option, which allows us to group the results by another column. We will be grouping by the createdAt column, which contains a timestamp of when the record was created. Trevor allows you to group them by day, week, month or year. We’ll group by day.

Assuming we have our sales \$ in a column called markup the end result looks something like this:

<img src="https://miro.medium.com/max/700/1*59c1p0bdK9MnL3uPaOcjWQ.png" />

Click Done. Notice that Trevor sorts the dates in descending order, but we actually want them in ascending order so that we can build correct formulas in Google Sheets. You can sort the column by clicking the little arrow next to the column name, and clicking “sort by”.

The next step is to click Save. Give your report a name, and click Save again. Next in the popup, click “Live stream results to Google Sheets”.

Copy the link that shows up, and then open up a new Google Sheet.

## Using Google Sheets to group your data

Paste the value you just copied, and voila, the sheet is populated with data from your database!
Note: if your dates are showing up as numbers, select the column and click Format -> Numbers -> Date.

Great! Now all you have to do is group the data for the last 7 days. Luckily, Sheets is pretty powerful too.

Next to your list of results, create two new columns, called date and number.

In the date column, start at the top by typing in `TODAY()-7` Google Sheets will interpret this as todays date minus 7 days, so you should see last weeks date show up.

In the rows below that, add the same, but change the numbers counting down to 1. So you have `TODAY()-6`, `TODAY()-5` and so on.

Then in the column right next to it, we’ll use the `LOOKUP` function to lookup the date from the database data delivered by Trevor, and return the corresponding number.

In the first row, type `LOOKUP(TODAY()-7,A1:A500,B1:B500)`. This only works if you have pasted your Trevor link in the top left box. If not, you’ll have to change the A and B values. The lookup functions works like this: `TODAY()-7` tells it what to look for, `A1:A500` is the range you want to look in and `B1:B500` is where the Sheet will grab the corresponding value from.

You’ll end up with something like this:

<img src="https://miro.medium.com/max/700/1*UuYW-XYtbgi-2sw92EaIUA.png" />

The sum part at the bottom is created by typing `SUM(E3:E8)`. This is the total number for the last 7 days.

You can apply the same concept for the last 30 days and quarter to date. Because you have the numbers per day too, we can also create line charts instead of only raw numbers.

Important: Google Sheets doesn’t automatically update this data. You have to add a Google Script.

Geckoboard has written an excellent article on how to do this, which can be fond here: [link](https://support.geckoboard.com/hc/en-us/articles/216438097-Use-Google-Sheets-ImportData-function-to-display-data-in-Geckoboard). Click through to the “Step-by-step guide: how to automatically update your data”.

In the `setValue` part, make sure you paste the value you got from Trevor which you pasted in the sheet.

I suggest setting the auto update to 15 minutes, but you can choose any value you like.
Once you’ve done that, we can move on to the final part.

That’s it! When you click “Send Request” it should use your proxy.

## Using Geckoboard to display your data

The final part is using [Geckoboard](https://geckoboard.com) to display your data.

You can use other reporting tools that support Google Sheets too, but we’ve found that Geckoboard works the best.

Click “Add Widget”, then “Spreadsheet”. After connecting your Google account, select the sheet you’ve been working in.

Let’s add a rev counter first. Select “Geck-o-meter” at the top. For value, you can enter the box which contains the sum. In our case, thats `E11`. You can also do this by clicking in the sheet preview in the bottom right.

It should look like this (I’ve blurred the actual numbers):

<img src="https://miro.medium.com/max/700/1*Lbfz7-jMgjmA4pzH8pFI5w.png" />

If you want to add a line-chart, change the type to line-chart. You see you’ll now get two values to enter, the X-axis and the Y-axis.

For X-axis, enter `D3:D9` or drag the dates you want to select. For the Y-axis, enter `E3:E9` or drag them as well. You should see something like (values blurred again):

<img src="https://miro.medium.com/max/700/1*2S1FpUHKBK9XUJAJT-FeJA.png" />

The beauty of automating the dates in Sheets is that Gecko will automatically show the correct time-period too.

There’s far more advanced stuff you can now do by applying the same concepts. You can add multiple reports from Trevor into the same sheet for instance, or show the last 7 days versus the 7 days before that, by adding a new set of columns showing those values.

Let me know if you’ve found this helpful! Best of luck building your dashboard 💪
