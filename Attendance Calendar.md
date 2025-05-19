To save on performance of loading the calendar numbers, there are two methods.

1) Limit the query scope to current date week and week beyond that are only made when user click on the "view" button to load that week.
2) Store months records in another table therefore the numbers are quick to query by id matching and no further processing is required.

Caveat with solution 2) you have to run a cron job that updates changes made on a daily basis except for the current day (current data should be live data).