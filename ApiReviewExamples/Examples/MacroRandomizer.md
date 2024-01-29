# API Example: Macro Randomizer
This website generates random [image macro](https://en.wiktionary.org/wiki/image_macro)s. It pulls a random bit of text from a variety of text-based APIs, then pulls a random image from a variety of different image APIs, and puts them together using a text-image-overlay API. This is certainly the most complex example in the lesson, but it is also the most powerful; combining multiple APIs can be quite interesting.

- [Preview: https://macrorandomizer.hylandoutreach.repl.co/](https://macrorandomizer.hylandoutreach.repl.co/)
- [Project: https://replit.com/@HylandOutreach/MacroRandomizer](https://replit.com/@HylandOutreach/MacroRandomizer)
- APIs: Several

## Improvement Ideas
This site is already fairly functional, but of course, there are ways to improve it.

### Option Selections
Currently, the image that loads has a few options hardcoded in the `getImageWithText` function. These include:

- `overlayColor` - set to a random color hex code
- `textColor` - set to white (hex+alpha code)
- `textSize` - set to 32

The query parameters also include `x_align`, `y_align`, and `margin` - these generally make the image appear nicer. However, it may be a good idea to allow the user to change these from the default values if they would like!

Add [number inputs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number) and [color pickers](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/color) to the site to allow the user to decide some of these options.

### Text & Image Sources
Currently, the text and image sources are chosen randomly; the page will simply pick a random API, and make a request. Instead of doing this, allow the _user_ to decide which sources to use for the text and images!

This can be done via HTML dropdowns.

### Style Updates
Currently, the styles for the website are pretty lacking. Make the page look better. Feel free to do whatever you'd like, but here are some ideas:

- Center the button and image
- Remove the border when there is no image (e.g., right when the page loads)
- Make the button look cooler
- Dynamically update the image size so it fits better

### Broken Images
Currently, some images are broken. Do some debugging to figure out what that is happening, and fix it!

### Progress
Currently, the loading indicator simply spins (and it takes a _very_ long time sometimes). Instead of simply watching the indicator spin, create some sort of progress indicator based on which part of the code is currently running. This could be as simple as adding a `<p>` element to the page every time a new request is about to happen, with some information about which request is running - or it could be an [actual progress bar](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress).

## API Information
There are so many different APIs used to create this website.

### Text Generation
Each of these APIs return some sort of text.

#### Advice Slips
The [Advice Slip API](https://api.adviceslip.com/advice) returns a piece of advice. The JSON looks something like this:

```json
{
  "slip": {
    "id": 9,
    "advice": "True happiness always resides in the quest."
  }
}
```

The actual text is available through the `obj.slip.advice` property.

#### MeowFacts
The [MeowFacts API](https://meowfacts.herokuapp.com/) returns a fact about a cat. The JSON looks something like this:


```json
{
  "data": [
    "Cats can jump up to six times their length."
  ]
}
```

The actual text is available through the `obj.data[0]` value.

#### Random Quotes
The [Quote Garden API](https://quote-garden.onrender.com/api/v3/quotes/random) returns a random quote and author. The JSON looks something like this:

```json
{
  "statusCode": 200,
  "message": "Random quotes",
  "pagination": {
    "currentPage": 1,
    "nextPage": null,
    "totalPages": 1
  },
  "totalQuotes": 1,
  "data": [
    {
      "_id": "5eb17ab1b69dc744b4e7b124",
      "quoteText": "The purpose of life is a life of purpose.",
      "quoteAuthor": "Robert Byrne",
      "quoteGenre": "life",
      "__v": 0
    }
  ]
}
```

The actual text is available through `obj.data[0].quoteText`, and the author is available through `obj.data[0].quoteAuthor`.

#### Stoic Quotes
The [Stoic Quotes API](https://api.themotivate365.com/stoic-quote) returns a random stoic quote. The JSON looks something like this:

```json
{
  "author": "TheStoicEmperor",
  "quote": "That which we desire lies across an ocean of hard won knowledge."
}
```

The actual text is available through `obj.quote`.

### Image Generation
There are a few different ways the code gets images.

#### The Metropolitan Museum of Art
The [Met API](https://metmuseum.github.io/) is the most complex in this lesson, mostly because it requires multiple API calls. The first request searches the collection, and returns a list of Object IDs.

Here is an example URL:

[https://collectionapi.metmuseum.org/public/collection/v1/search?q=you can search for anything and it doesnt really matter&hasImages=true](https://collectionapi.metmuseum.org/public/collection/v1/search?q=you%20can%20search%20for%20anything%20and%20it%20doesnt%20really%20matter&hasImages=true)

The response looks something like this:

```json
{
  "total":23,
  "objectIDs":[459027,459186,437854,438821,435621,36131,459028,435848,53660,485416,39901,435809,436485,436453,72774,665702,482518,488978,206332,451263,828241,40057,39895]
}
```

From there, one random element from the `obj.objectIDs` array can be chosen, and used in the _next_ API call. The next call gets information about the object.

Here is an example URL:

[https://collectionapi.metmuseum.org/public/collection/v1/objects/459027](https://collectionapi.metmuseum.org/public/collection/v1/objects/459027)

The response looks something like this (but with a lot more data):

```json
{
  "objectID": 459027,
  "isHighlight": true,
  "accessionNumber": "1975.1.85",
  "accessionYear": "1975",
  "isPublicDomain": true,
  "primaryImage": "https://images.metmuseum.org/CRDImages/rl/original/DP221483.jpg",
  "primaryImageSmall": "https://images.metmuseum.org/CRDImages/rl/web-large/DP221483.jpg",
  "moreStuff": "thereseabunchmore...."
}
```

From there, the actual image is retrieved through the `obj.primaryImageSmall` property. For example, something like this:

![](../Assets/DP221483.jpg)

#### shibe.online
The [shibe.online API](https://shibe.online/) is thankfully much simpler. This is the same API used in the [Dog Fetcher](../../ApiConsumption/DogFetcherCodeAlong.md) activity.

The URL looks like this: [https://shibe.online/api/shibes?count=1](https://shibe.online/api/shibes?count=1)

The JSON response looks like this:

```json
["https://cdn.shibe.online/shibes/1ea85ce4b152725f5e69f5996b5fa31cb7015576.jpg"]
```

The actual image URL is retrievable through `obj[0]` and looks something like this:

![](../Assets/Shibes.jpg)

#### cataas
The [cataas API](https://cataas.com/#/) is even _more_ simple. This is the same API used in the [Cat Says](../CatSayCodeAlong.md) activity. It does not even require a `fetch` request - it simply returns a random image with the same URL every time.

The URL looks like this: [https://cataas.com/cat](https://cataas.com/cat)

The actual image can be something like this:

![](../Assets/Cat.jpg)

### Text Over Image API
This is where the magic happens. The [Text Over Image API](https://textoverimage.moesif.com/) takes an image, and some text, and some other parameters, and creates a new image with the text on top of the image. There is no JSON, and no `fetch` - it is another example of a URL that returns an image directly. Query parameters include:

- `image_url`: the URL for the image (generated randomly in this case)
- `overlay_color`: a hex+alpha value to use as an overlay layer in the image (generated randomly in this case)
- `text`: the text to put on top of the image (generated randomly in this case)
- `text_color`: the color of the text (set to white by default)
- `text_size`: the size of the text (set to 32 by default)
- `x_align`: the horizontal alignment of the text (centered by default)
- `y_align`: the vertical alignment of the text (centered by default)
- `margin`: space around the text (20 by default)

All of these come together to create the new image!

## Code Information
The code for this project is quite involved. There are several functions in the **script.js** file, and many of them are stored in variables within arrays and called dynamically.

- `randomFromArray`: a helper function to choose a random item from an array
- `getAdvice`: a function to call the advice slip API, and return the text
- `getCatFact` a function to call the mew facts API, and return the text
- `getRandomQuote`: a function to call the quote garden API, and return the text
- `getStoicQuote`: a function to call the stoic quote API, and return th etext
- `getMetImage`: a function that gets a random image URL using the Met API
- `getDogImage`: a function to call the shibe.online API and return the URL for the image
- `getCatImage`: a function to return a random cat image URL through the cataas API
- `textGenFunctions`: an array containing all the functions that generate text
- `imageGenFunctions:` an array containing all the functions that generate images
- `getText`: a function that chooses a random text-generating function, calls it, and returns the result
- `getImage`: a function that chooses a random image-generating function, calls it, and returns the result
- `getImageWithText`: a function that generates a random image, random text, and calls the Text Over Image API with the values
- `newRandomImage`: the function that runs when the "New Random Image" button is clicked - it generates a new image and sets it on the page
