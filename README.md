# crowdsensing_datasets

Comparison of datasets:

| Name                                   | Purpose                | Start Date | End Date   | Number of examples | Number of crowd sensors (for crowd level regression) | Number of unique users | Number of events (for event-detection) | Number of non-events (for event-detection) |
| -------------------------------------- | ---------------------- | ---------- | ---------- | ------------------ | ---------------------------------------------------- | ---------------------- | -------------------------------------- | ------------------------------------------ |
| Sensor Counts (Melbourne)              | Source                 | 2009-05-01 | 2020-04-30 | 3132346            | 66                                                   | -                      | -                                      | -                                          |
| Tweets (Melbourne)                     | Source                 | 2010-09-12 | 2018-06-04 | 266931             | -                                                    | 20176                  | -                                      | -                                          |
| Tweets (max 100 duplicate coordinates) | Crowd Level Regression | 2010-09-21 | 2018-02-02 | 24638              | 42                                                   | 5659                   | -                                      | -                                          |
| Tweets (max 10 duplicate coordinates)  | Crowd Level Regression | 2010-09-21 | 2018-02-02 | 12801              | 42                                                   | 3785                   | -                                      | -                                          |
| Flickr (near to Town Hall (West))      | Crowd Level Regression | 2010-07-08 | 2020-03-29 | 6076               | -                                                    | 852                    | -                                      | -                                          |
| Tweets (is _event tagged)              | Event detection        | 2014-01-12 | 2018-02-12 | 1393561            | -                                                    | 77642                  | 22241                                  | 1371320                                    |

A brief overview of how these datasets were derived and how they are categorized:

Tweets for regression
- sources:
	- userVisits-Melb-tweets-280518.csv (original tweet dataset)
- sorted by date, cleaned:
	- tweets_unfiltered.csv
- filtered for duplicate coordinates, and tagged to nearest counting sensors:
	- tweets_max10_duplicate_coords.csv
	- tweets_max100_duplicate_coords.csv

Pedestrian Counts and Sensors
- sources:
	- Pedestrian_Counting_System__2009_to_Present_counts_per_hour_.csv (from melb gov)
	- Pedestrian_Counting_System_-_Sensor_Locations.csv (from melb gov)
- sensor locations, cleaned:
	- sensor_locations.csv
- pedestrian counts tagged to corresponding sensors:
	- counts_withsensors.csv


Flickr
- sources: flickr crawler
- crawled for flickr posts within 100m of the counting sensor at Melbourne Town Hall (West) 
[-37.81487988, 144.9660878]
	- flickr_near_townhallwest


Event Detection
- sources:
	- Event_permits_2014-2018_including_film_shoots_photoshoots_weddings_Christmas_parties_
	  promotions__fun_runs_and_public_events.csv (from melb gov)
	- getOldTweets crawler
	- tweets_unfiltered.csv
- cleaned event permits dataset, filtered for public events, and geotagged to POIs (if available)
	- events_geo_tagged_public.csv
- used getOldTweets to crawl for tweets within 100m of each event in the above dataset:
	- tweets_withevent.csv
- merged with tweets_unfiltered.csv (superset of all melb tweets) to label tweets as is_event True or False
	- tweets_isevent_tagged.csv
	- Note: due to GitHub file size restrictions the dataset will be placed here: https://tinyurl.com/tweets-isevent

