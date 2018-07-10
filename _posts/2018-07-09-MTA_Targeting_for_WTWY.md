# MTA Targets for WTWY Gala Campaign

For the first week of Metis, we were given the opportunity to assist WomenTechWomenYes with their campaign targeting. WomenTechWomenYes will be hosting a gala fundraiser and will be looking to stage teams at MTA stations to solicit email addressses as well as sell tickets for the gala. Our task is to use data to provide a list of MTA stations for WTWY to reach their target audience. 

# The Data

To start our analysis, we pulled turnstile data from the [MTA website](http://web.mta.info/developers/turnstile.html). Of course, there were issues with the data and we had to correct it. We made the following assumptions to clean the data. 

  - There were counters that went down instead of up. We made the assumption these counters were going in reverse.
  - Some counters were reset, which resulted in very large differences between counts. We eliminated these values by setting them to zero. 
  - There were multiple stations with the same name, we assumed that all stations that shared a name were the same station for the purpose of this study.

# A First Look
After cleaning the data, we charted the top 10 stations by traffic. 

With that data, we looked at the map to make some iniital guesses at which stations we thought would be best. Here is the map with the top 10 stations circled and the Gala location identified. 

Our initial hypothesis were 
  - *Grand Central Station - 42nd St*
  - *14th St - Union Square*
  - *Fulton St*
  
These assumptions were based on these stations being in the top 10 as well as distance to the Gala's location.

# Refining the Targeting Method

To refine our targets, we identified additional factors that we believed were associated with WTWY's targets, people who would attend the Gala and donate. We used census data and brought in the following details for the areas around our stations. 
   
   - *# of Women*
   - *Median Household Income*
   - *# of Bachelor Degrees*
   - *# of Graduate Degrees*
   - *Distance to the Gala*

Since census data is divided up by GeoIDs, we merged our datasets by correleating latitude and longitude of each station to their corresponding GeoID.

After joining our data, we made our initial model. We made all weights eqaul and quickly realized the top 10 stations by traffic seemed to keep that ranking. We made adjustments to the weighting scale to account for level of importance as well as the total range of the data. We produced the following recommendation index model from our data. 

- Recommendation Index = (
		3 x (min distance to Gala / Distance to Gala)
		2.5 x (# of Women / max # of Women)
		2 x (# of Entries / max # of Entries)
		1.4 x (# of Bachelor Degrees / max # of Bach. Degrees)
		1.3 x (Avg household income / max avg household income)
		1.1 x (# of Graduate Degrees / max # of Grad Degrees)
	)* 100 / 11.3

# Recommendations

Our model produced these top 3 stations.

- *East Broadway* - #2 in Distance to Gala, #2 in Population of Women
- *Grand Central - 42nd St* - #1 in MTA traffic, #1 in Income/Education
- *86th St* - #3 in Population of Women, #7 in MTA traffic

Since the distance to the Gala and population of women were weighted highly, we saw East Broadway become an interesting target. Grand Central was expected with its extremely high traffic. 86th St was also a surprise as it was farther away from the gala than other stations, but it's area's high number of women and high MTA traffic made that a good target as well. When we look at these 3 stations, it spans a large distance across Manhattan which make them great choices.

