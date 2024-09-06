# API Example: Weather App
This site takes a search location (either zip code or city name), finds some information about the current weather for it, and displays it.

- [Preview](https://hylandtechclub.com/showcase/Web103/Weather/index.html)
- [Project: https://glitch.com/edit/#!/weather-api-app-thing](https://glitch.com/edit/#!/weather-api-app-thing)
- [APIs: Open-Meteo](https://open-meteo.com/)

## Improvement Ideas
There are a ton of ways this site could be improved!

### New Pictures
Currently, there are five pictures available. Each picture corresponds to a set of [weather codes](https://open-meteo.com/en/docs#weathervariables). In the **script.js** file, these images are defined within the `weatherCodeImages` array.

Start by adding more pictures for different types of weather! For example, right now, all "rainy" weather codes are grouped together - but there are specific codes that could have different images! This could be things like:

- Drizzling
- Freezing Rain
- Pouring Down Rain
- Thunderstorms

There are also some different options for snow - it could be heavy or light.

#### Pictures Based on Day/Night
This would be more of a challenge, but it could be cool. Figure out if it is daytime or nighttime in the current region, and adjust the images accordingly. For example, snow during the day could look like this:

![](../Assets/SnowFallDay.gif)

And snow during the night could look like this:

![](https://i.pinimg.com/originals/63/31/dc/6331dca048b6b595be53df8a279646a3.gif)

There could even be specific images for different types of cities (rural/urban, based on population), different temperatures (hot day v. cold day), and so on.

_Note: the `time` is returned as part of the `current_weather` object.

### More Location Information
Currently, when searching by zip code or city, the main name of the location is displayed on the page. However, there is a lot more information that could appear!

When finding the data in the `getDataFromSearchLocation` function, the response contains several properties in addition to the latitude, longitude, and name. These include:

- `admin1` - state
- `admin2` - county
- `country`
- `elevation`
- `population`
- `postcodes`

Add some of this to the page!

### Loading Indicator
Currently, when entering a new search term, there is no indication that the page is waiting for a response. Add a loading indicator that appears before the request, and disappears after the request completes!

### Historical Data
It could be cool to get some information about what weather was on this day one year ago - this is possible with the [Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api#latitude=41.48&longitude=-81.80&start_date=2022-03-29&end_date=2022-03-29&daily=temperature_2m_max&timezone=auto&temperature_unit=fahrenheit)!

A request URL could look something like this (for the given latitude, longitude, and current date):

[https://open-meteo.com/en/docs/historical-weather-api#latitude=41.48&longitude=-81.80&start_date=2022-03-29&end_date=2022-03-29&daily=temperature_2m_max&timezone=auto&temperature_unit=fahrenheit](https://open-meteo.com/en/docs/historical-weather-api#latitude=41.48&longitude=-81.80&start_date=2022-03-29&end_date=2022-03-29&daily=temperature_2m_max&timezone=auto&temperature_unit=fahrenheit)

Figure out how to get the current date in JavaScript, make the request, and add the data to the page!

## API Information
The [Open-Meteo site](https://open-meteo.com/) has a ton of neat APIs that are capable of doing quite a few things.

### Geocoding API
The [Geocoding API](https://open-meteo.com/en/docs/geocoding-api) can get data about a location based on a search. This is used to turn the search term on the site into a latitude, longitude, and name.

### Weather Forecast API
The [Weather Forecast API](https://open-meteo.com/en/docs) is a bit more complex - there are a ton of different parameters and features available. The current site only really cares about the current weather, but it is possible to get an hourly forecast, a daily forecast, information about precipitation, wind, soil moisture, sunrise, sunset... quite a bit of information.

Try to play around with the URL builder a bit to see what type of data you can get. There's a ton of it!

## Code Information
The code is fairly substantial for this website. Most of the interesting bits are in the **script.js** file:

- `weatherCodeImages`: an array of objects, each mapping an image URL to a group of [weather codes](https://open-meteo.com/en/docs#weathervariables)
- `getImageUrlForWeatherCode`: a function that takes a weather code, and returns the image URL for that weather code
- `setBgFromWeatherCode`: a function that takes a weather code, and sets the background image to the picture for the code
- `getDataFromSearchLocation`: a function that takes a search term (e.g., "44107" or "Los Angeles"), and finds location information for the term including latitude and longitude
    - This uses the [Geocoding API](https://open-meteo.com/en/docs/geocoding-api)
- `getWeatherFromLatLng`: a function that takes a latitude and longitude, and gets the current weather for the location
    - This uses the [Weather Forecast API](https://open-meteo.com/en/docs)
- `getWeather`: the function that runs when the "Get Weather" button is clicked; it grabs the value from the search box, finds the weather for the location, and displays it on the page

