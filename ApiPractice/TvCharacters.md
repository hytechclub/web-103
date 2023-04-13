# TV Characters
Follow these instructions to update a website that displays characters from TV shows.

[Click here to view the TV Characters Starter Repl project.](https://replit.com/@HylandOutreach/TvCharacters) Fork the project to begin the activity.

## Part Zero: Background
There is significant code and functionality already built into this project.

### The User Experience
When someone goes to the page, they are able to click the "Load Characters" button to see characters from Stranger Things appear.

### The API
The API that makes this possible is named [TVMAZE](https://www.tvmaze.com/api). There are a variety of endpoints that return data about TV shows. The TV Characters site uses the `/singlesearch/` endpoint to get data about `Stranger Things`, and the `cast` data is embedded. The URL is static, so it currently returns the same data each time. It looks something like this:

#### URL
[https://api.tvmaze.com/singlesearch/shows?q=Stranger Things&embed=cast](https://api.tvmaze.com/singlesearch/shows?q=Stranger%20Things&embed=cast)

#### Response (Abbreviated)
```json
{
	"id": 2993,
	"url": "https://www.tvmaze.com/shows/2993/stranger-things",
	"name": "Stranger Things",
	"summary": "<p>A love letter to the '80s classics that captivated a generation, <b>Stranger Things</b> is set in 1983 Indiana, where a young boy vanishes into thin air. As friends, family and local police search for answers, they are drawn into an extraordinary mystery involving top-secret government experiments, terrifying supernatural forces and one very strange little girl.</p>",
	"_embedded": {
		"cast": [
      {
				"person": {
					"name": "Winona Ryder",
					"image": {
						"medium": "https://static.tvmaze.com/uploads/images/medium_portrait/204/511427.jpg"
					}
				},
				"character": {
					"name": "Joyce Byers",
					"image": {
						"medium": "https://static.tvmaze.com/uploads/images/medium_portrait/406/1015330.jpg"
					}
				}
			},
			{
				"person": {
					"name": "Caleb McLaughlin",
					"image": {
						"medium": "https://static.tvmaze.com/uploads/images/medium_portrait/16/40907.jpg"
					}
				},
				"character": {
					"name": "Lucas Sinclair",
					"image": {
						"medium": "https://static.tvmaze.com/uploads/images/medium_portrait/410/1027426.jpg"
					}
				}
			}
		]
	}
}
```

All the data that renders is in the `_embedded.cast` array property.

### The Code
There are several functions in the **script.js** file that make the current site work how it does.

- `objectToHtml`: takes a JSON data object and returns an HTML element with a nice image/name
- `getCharactersForShow`: makes the request to the API - currently returns information about Stranger Things
- `loadCharacters`: makes the call to get the data, and then puts it on the page

### The Goal
Right now, the site is exclusively about Stranger Things. Update it so that it can display characters from any TV show!

## Part One: The HTML
First, there needs to be a way for the user to say which TV show they would like.

1. Open the **index.html** file for editing
1. Make a new line under the `<h1>Characters</h1>` element
1. There, create a new `<input>` element
1. Set the `type` attribute to be `"text"`
1. Set the `id` attribute to be `"tv-show"`
1. Set the `placeholder` attribute to be `"Enter a TV Show"`

Run the project and verify that the new text box appears! The added HTML should look like this:

```html
<input id="tv-show" placeholder="Enter a TV Show" />
```

## Part Two: Function Parameterization
Next, the JavaScript code needs to take what the user enters, and pass it along to get the data.

### Updating the Definition
Currently, the `getCharactersForShow` function does _not_ take any arguments. Add a parameter so that it will be possible to pass a show search query into the API.

1. Open the **script.js** file for editing
1. Find the `getCharactersForShow` function definition
1. Add a parameter named `show` between the parentheses

The updated code should look like this:

```js
async function getCharactersForShow(show) { /* ... */ }
```

### Updating the Call
Now, it will be possible to pass the value to the function call.

1. Find the `loadCharacters` function definition
1. Make a new line above the `characters` variable creation
1. There, create a new variable named `tvShowInput`
1. Use `document.querySelector` to grab the `<input id="tv-show">` from the HTML, and store it in the `tvShowInput` variable
1. Under that, create a new variable named `tvShow`
1. Set `tvShow` to be the `value` of `tvShowInput`
1. Under that, update the call to `getCharactersForShow` by passing `tvShow` as an argument

Nothing will actually change yet, but now the `getCharactersForShow` function has a show to use! The updated code should look something like this:

```js
let tvShowInput = document.querySelector("#tv-show");
let tvShow = tvShowInput.value;
let characters = await getCharactersForShow(tvShow);
```

## Part Three: Query Parameterization
Here's where the magic happens. The API call can be updated to search for whatever show the user entered in the text box!

1. Find the `getCharactersForShow` function
1. Find the `url` variable creation
1. In the template literal for it, remove `Stranger Things`
1. Replace it with the interpolated value of the `show` parameter

Run the project, enter a real TV show, click the button, and verify that characters from that TV show appear! The updated URL code should look something like this:

```js
let url = `https://api.tvmaze.com/singlesearch/shows?q=${show}&embed=cast`;
```

## Part Four: Handling an Error
Now this is all well and good, but what happens when a fake show title is entered? Luckily, there is a `try`/`catch` in place, so a message like `TypeError: Cannot read properties of null (reading '_embedded')` may be `alert`ed. That message is not very clear, though... the site can do better.

### Background
HTTP responses have [status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) that indicate the success of the request. For example, a [404](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404) error indicates that a resource has not been found. In the case of the TVMAZE API, it will return a `404` response if a TV search does not return any results.

The status code is returned with the response object from a `fetch` call, so it is possible to check it. It is also possible to use [`throw`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw) to display a new message to bubble up in the `try`/`catch`.

The goal will be to display a new message if the search fails, and the entered show is not found!

### The Code
After the response is returned, it will be possible to handle any errors gracefully.

1. Open the **script.js** file for editing
1. Find the `getCharactersForShow` function definition
1. Find the `fetch` call in the `try` block
1. Make a new line under that
1. There, create an `if` structure
1. In the `if` condition, check if `response.status` is equal to `404`
1. In the body block of the `if` statement, use `throw` to send an error message of "Show not found ☹"

Now, run the project, enter a fake show, and verify that a nicer error message is `alert`ed! The added code should look something like this:

```js
if (response.status === 404) {
  throw `Show not found ☹`;
}
```

## Conclusion
This activity showed another example of an API with a lot of possibility. The code only used a small part of the data returned, but so much more of it could be useful! Here are some ideas for this API:

- Display both the character _and_ the actor for each entry
- Display more information about each new show, such as the description or the image
- Update the CSS colors/fonts so that they are not specific to Stranger Things
- Make each character "card" a link that can go to the character page (like [this](https://www.tvmaze.com/characters/165115/stranger-things-mike-wheeler))

Feel free to use the API for any desired purpose.
