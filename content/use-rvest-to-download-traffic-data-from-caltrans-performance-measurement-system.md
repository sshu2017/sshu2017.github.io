Title: Use Rvest to Download Traffic Data from Caltrans Performance Measurement System
Date: 2016-08-08 07:29
Author: sshu
Category: R, web-scraping
Slug: use-rvest-to-download-traffic-data-from-caltrans-performance-measurement-system
Status: published

Recently I helped a friend of mine to download some traffic time-series data from the [Caltrans Performance Measurement System](http://pems.dot.ca.gov/). Basically we need to download the traffic data from all the major traffic census stations on the I-405 freeway, and the time span needs to cover a couple of months. After searching online for a couple of days and asking a few questions on [stackoverflow](http://stackoverflow.com/) ([1](http://stackoverflow.com/questions/28418770/using-rvest-or-httr-to-log-in-to-non-standard-forms-on-a-webpage),[2](http://stackoverflow.com/questions/38687068/with-rvest-how-to-extract-html-contents-from-the-object-returned-by-submit-form),[3](http://stackoverflow.com/questions/38759663/how-to-reuse-a-session-to-avoid-repeated-login-when-scraping-with-rvest)) I finally assembled a piece of R code to accomplish what we need to do.

``` R

rm(list=ls())
library(rvest)
library(httr)

getTable <- function(resp){
  # This function extract the table from a response
  pg <- content(resp$response)
  html_nodes(pg, 'table.inlayTable') %>% html_table() -> tab
  return(tab) # return the content of table
}

generateURL <- function(siteID){
  # This function generates a URL for each input siteID
  urlPart1 = "http://pems.dot.ca.gov/?report_form=1&dnode=tmgs&content=tmg_volumes&tab=tmg_vol_ts&export=&tmg_station_id="
  urlPart2 = "&s_time_id=1369094400&s_time_id_f=05%2F21%2F2013&e_time_id=1371772740&e_time_id_f=06%2F20%2F2013&tod=all&tod_from=0&tod_to=0&dow_5=on&dow_6=on&tmg_sub_id=all&q=obs_flow&gn=hour&html.x=34&html.y=8"
  url = paste(urlPart1, toString(siteID), urlPart2, sep = '')
  return (url)
}

siteIDList = c(74250, 75020, 74020)
mainURL = "http://pems.dot.ca.gov/"
pgsession <- html_session(mainURL)
pgform <- html_form(pgsession)[[1]]
filled_form <- set_values(pgform,
                          'username' = 'segoviashu2000@yahoo.com',
                          'password' = 'house6y')

# slog is the logged-in session that can be reused
slog <- submit_form(pgsession, filled_form) 

# loop thru siteIDList to scrape all the tables
vectorOfTables <- vector(mode = 'list', length = length(siteIDList))
i = 1
for (siteID in siteIDList){
   print ("Working on site:", quote = F)
   print (siteID)
   newsession = jump_to(slog, generateURL(siteID))
   vectorOfTables[i] = getTable(newsession)
   i = i+1
}

# Show the first table in vectorOfTables
vectorOfTables[1]
```

And remember to always use caution when scarping!
