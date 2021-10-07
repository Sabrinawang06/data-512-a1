
#DATA 512 Assignment 1: Data Curation

The goal of this assignment is to construct, analyze, and publish a dataset of monthly traffic on English Wikipedia from December 1, 2007 through September 30, 2021. This project provides insights on how users' preference on different accessing platform changes overtime. 

There are two different [Wikimedia REST API endpoints](https://www.mediawiki.org/wiki/REST_API) used by Wikipedia from 2007 to 2021:
* The Legacy Pagecounts API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end) provides access to desktop and mobile traffic data from December 2007 through July 2016.
* The Pageviews API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month.


There are step major steps in the analysis: 
* Data Acquisition
  * The data is obtained using the sample code provided in this [notebook](http://paws-public.wmflabs.org/paws-public/User:Jtmorgan/data512_a1_example.ipynb) with modification of the parameters
  * Five json files are created and stored under the "data" folder. Each json file obtain the raw output of the API queries containing the monthly view information under each API and access platform setting
* Data Processing
  * The data obtained from the API queries is cleaned and processed
    * For data collected from the Pageviews API, monthly values for mobile-app and mobile-web are combined to create a total mobile traffic count for each month
    * For all data, the value of timestamp are seperated into four-digit year (YYYY) and two-digit month (MM) and values for day and hour (DDHH) are discarded
  * The processed data is organized into a tabular format and saved as a .csv filed named en-wikipedia_traffic_200712-202109.csv stored under the "data" folder. For months with 0 views are filled with number 0.
      * Year: the year of which the number of views is occured
      * Month: the month of which the number of views is occured
      * pagecount_all_views: the total views of both platform (desktop and mobile) for Pagecount API for that specific month/year
      * pagecount_desktop_views: the total views of desktop access only for Pagecount API for that specific month/year
      * pagecount_mobile_views: the total views of mobile access only for Pagecount API for that specific month/year
      * pageview_all_views: the total views of both platform (desktop and mobile) for Pageview API for that specific month/year
      * pageview_desktop_views: the total views of desktop access only for Pageview API for that specific month/year
      * pageview_mobile_views: the total views of mobile access only (combination ofr mobile website and mobile app) for Pageview API for that specific month/year
      
| Column                  | Value     |
|-------------------------|-----------|
| year                    | YYYY      |
| month                   | MM        |
| pagecount_all_views     | num_views |
| pagecount_desktop_views | num_views |
| pagecount_mobile_views  | num_views |
| pageview_all_views      | num_views |
| pageview_desktop_views  | num_views |


* Analysis
  * A time series plot is created to show the overall trend of changing in views for each API (all_views) and each access platform under each API (desktop_views, mobile_views). The output plot is saved as a .png file named "traffic.png"
  ![traffic analysis](https://github.com/Sabrinawang06/data-512-a1/blob/3ea2d68cd4adae00d4c82f677f3402f3976adeea/traffic.png)
  * Two additional plots are created; one for each API so that the trend can be views seperately. 


Notes: 
1. Data from the Pageview API excludes spiders/crawlers, while data from the Pagecounts API does not
2. The scope of the data included used in this project is from December 2007 (including the whole month of December) to September 2021 (including the whole month of September)
