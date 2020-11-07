# Top Cities To Own and Electric Car

## Census

Our program starts by executing the Census_Population.ipynb file in the Census folder. This notebook performs the following operations:

1. Makes a call to the Census API for city and city population. The data that is retunred is stored in a dataframe called census_df.
2. Prints the total number of cities in the census_df dataset.
3. Creates a df called big_city_df which only includes cities where the population is over 250k.
4. Prints the number of big cities to the screen.
5. Creates a data frame names City_State which holds the values of the split city name so that city and state are in one columns.
6. Merges the big_city_df dataframe with the City_State dataframe in city_merge_df.
7. Renames the newly merged columns from City_State as Clean_City and Clean_State
8. Creates a new column in city_merge_df called City_State which is the concatenation of the column Clean_City and a comma and Clean_State. 
9. Creates blank columns for Lat and Lng in the city_merge_df
9. Loops trough city_merge_df and retrieves Lat and Lng by passing City_State to the api request.
10. Prints a log of what was loaded and what was not loaded to the screen.
11. Creates a df called final_city_df which holds columns for City_State, Clean_City, Population, Lat, and Lng.
12. Generates a csv file of the final_city_df to the Resources folder.
13. Generates a bar chart of the top 10 cities by largest population to the Resources folder.
14. Creates a heat map of the cities weighted by population. Output place in the Resources folder.
15. Generates a boxplot of population to the Resources folder.

## Weather

The Weather notebook picks up where the census notebook leaves off by performing the following operations:

1. Loads the census_city.csv file from the census notebook into the cities_pd dataframe.
2. Cleans the dataframe by deleting the "Unnamed: 0" column,
3. Create a blank Max Temp and a Min temp column in the cities_pd df.
4. Loops through the cities_pd df and makes an API call to the OpenWeather API, pulling max and min temp for each city and updating the appropriate fields in the cities_pd df with those values. The program also prints a log of the sucessful and unsucessful responses to the screen.
5. Saves a csv file of the cities_pd df.
6. Creates weather_cities_pd from the cities_pd data and excludes cities where max temp is greater than 80 degrees F and where min temp is less than 60 degrees F.
7. Creates a weather_city_final.csv file in the Resources folder to be used in the OpenCharge notebook to the Resources folder.
8. Creates a heatmap on the weather_cities_pd df using max temp as the weight to the Resources folder.
9. Creates a box plot max temp and min temp to the Resources folder.
10. Calculates IQR, upper and lower limits, and outliers for min temp.
11. Generates a regression test for population vs min temp to the Resources folder.
12. Generates a regression test for population vs max temp to the Resources folder.  


## OpenCharge
Now that we have narrowed down our cities list to those with weather conditions suitable for electric cars, we wanted to guage how much infrastructure exists to support electric car owners. A key part of this infrastructure is charging stations and how widespread they are throughout a city. We located the Open Charge Map API which tracks charging station data across the globe.

The open_charge.ipynb notebook does the following:
1. Loads the list of cities that meet the weather parameters
2. Loads the lat/longs into lists that can be used in the query for the OpenCharge Map API
3. Loops through the lat/long pairs for each city and retrieves a list of all charging stations in a 50-mile radius
4. Loads the station counts found into a dataframe that contains the census and weather data
5. Calculated 'Stations per Mile' and added to the dataframe
6. Sorted the data frame by the number of stations per city to help organize the generated visuals
7. Creates a heatmap of the station count by city
8. Creates a heatmap of the station count per mile
9. Creates a histogram showing how widespread charging infrastructue is in cities
10. Creates a plot comparing station count to population
11. Creates a histogram showing stations per mile by city
12. Output from OpenCharge is saved in the OpenCharge/Results folder

Analysis from OpenCharge info:
- Of the cities evaluated for the number of charging stations, 9 of the top 10 are in California (mostly in the Los Angeles and San Francisco metro areas)
- The same cities in California also have the highest station density per mile
- There are only a handful of cities with more than 1,000 chargers; most cities evaluated had 700 or less
- Findings saved to the Findings folder.

