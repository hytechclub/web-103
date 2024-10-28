# Self-Paced Work: Dog Fetcher Updates
Follow these instructions to make some updates to the Dog Fetcher website.

## 🐦 Birds & Cats 🐈
Dogs are cool. Dogs are _really_ cool. But it might be even cooler to show images of other animals too! Luckily, **give-me-dogs.glitch.me** has APIs for birds and cats in addition to dogs! Incorporate these into the Dog Fetcher site.

### Basic Challenge: Replace
The simple way to do this would be to replace the `dogs` URL with one that points to either `birds` or `cats`. Basically, the base URL should look something like this instead:

```
https://give-me-dogs.glitch.me/cats
```

Update the URL in the `fetch` call to grab images of a different kind of animal. Then, update all the HTML to reflect the new type of animal!

### Advanced Challenge: Select
The more complex, but more rewarding, version of this challenge is to _allow the user to select what type of animal they want to see_. Dynamically update the URL based on whatever they want! Follow these steps:

#### HTML
Make these updates in the **index.html** file:

1. Change everywhere it says "dogs" to say "animals" instead
1. Right under the `<h1>`, add a new `<p>`
1. In the `<p>`, create a `<span>` asking "What animal would you like to see?"
1. Under the `<span>`, add a [`<select>`](https://www.w3schools.com/tags/tag_select.asp) element
1. In the `<select>` element, add [`<option>`](https://www.w3schools.com/tags/tag_option.asp) elements for all of these:
    - Shibes
    - Birds
    - Cats
1. Add an `id` attribute to the `<select>` so it is identifiable in JavaScript
1. Add `value` attributes to each `<option>` so they can be retrieved

#### JavaScript
Make these updates in the **script.js** file:

1. Update all places where it says "dogs" to say "animals" instead, to match the HTML
1. [Get the selected animal option](https://www.w3schools.com/jsref/prop_select_value.asp) in the body of the function
1. In the `fetch` call URL, replace the `shibes` with the interpolated value from the selected option value

## New Dog Breeds
Currently, the website only shows shiba inu dogs. This is a good thing, but some people might want other types of dogs as well. Luckily, this is possible... but it required the use of a _different_ API.

### The [Dog CEO Dog API](https://dog.ceo/dog-api/)
Head over to the **[Dog API](https://dog.ceo/dog-api/)** page to see how to get random dogs of a variety of breeds! This is very similar to the **shibe.online** API, but it is a little different:

- The base URL is `https://dog.ceo/api/breeds/image/random`
- There is no `count` query parameter
- Instead of an array, The response is a JSON object with a `"message"` property
- Only _one_ dog image is returned

Update the code to use this new API instead of the **shibe.online** API!

### More Customization
Another benefit of the Dog API is that it is actually possible to specify a breed in the request. There are a number of ways to work with this data.

- [Check out the Documentation for the API](https://dog.ceo/dog-api/documentation/)
- [Check out the BREEDS LIST page to see how these requests can be used](https://dog.ceo/dog-api/breeds-list)

Choose a few different breeds, and allow the _user_ to select which dog breed they would like to see.

## EXTRA CHALLENGE: Locking Pictures
This is fun, but removing all the pictures every time new ones are retrieved is kind of sad. Figure out a way to keep around some of the `<img>` elements every time new images are grabbed! It should be possible for the user to select which pictures they would like to keep; all other pictures should be removed.

_Note: This challenge may be quite difficult._
