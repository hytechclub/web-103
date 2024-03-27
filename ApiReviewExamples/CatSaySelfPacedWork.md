# Self-Paced Work: What Does the Cat Say Now?
Continue to explore the [cataas API](https://cataas.com/#/) and the [TikTok Text-to-Speech API](https://weilbyte.github.io/tiktok-tts/) with these exercises.

## GIFs Only
[Is it pronounced gif? Or is it gif?](https://www.youtube.com/watch?v=Nrk8sqZfsgI) The world may never know. The one thing we can all agree on is that there are GIF images of cats on the internet. And luckily, the **cataas API** has a way to send them!

Do some research to figure out how to limit images returned by the API to only GIFs.

For an added challenge, add a checkbox in the HTML to see if the user would like GIFs or all images, and add the `/gif/` to the URL if the box is checked! Additionally, update the `speak` function so that, if a gif is being generated, it waits a little longer to speak. Or, figure out how to make it speak only after the new image has loaded.

## Cat Tags
Another cool thing the **cataas API** can do is search by tag. For example, to display _only_ cats where "cute" is a tag, just add `/cute` before `/says`!

Do some research and figure out how to find cats with certain tags.

For an added challenge, add another text box in the HTML, and allow the user to enter a tag. But what tags could they enter???

### All Tags
Amazingly, there is an cataas API endpoint that returns the complete list of tags for cat images. Go to [https://cataas.com/api/tags](https://cataas.com/api/tags) to see the full list.

There are a few options here:

- Copy the current list into the **script.js** file directly, and use it to check before sending requests
- Create a dropdown in the HTML with a few selected tags hard-coded into the page
- Use `fetch` to dynamically load up the full list of tags, and dynamically create a dropdown in the HTML so the user can choose between all available tags

Feel free to use the tags however you'd like!

## Cat Filters
One additional fun thing that can be appended to any URL is the use of image filters! These filters take an image and transform it in some way. There are several filters available:

- blur
- mono
- sepia
- negative
- paint
- pixel

The filter option is added to the URL as a query parameter! For example, a URL could look like this: [https://cataas.com/cat/cute/says/meow?filter=negative](https://cataas.com/cat/cute/says/meow?json=true&filter=negative)

There are some options here:

- Add a default filter to every image returned
- Add a _random_ filter to every image returned
- Allow the user to select a filter to apply to the image

Feel free to use filters however you'd like!

## New Voices
There are plenty of TikTok voices to try. Figure out how to swap out the Rocket voice for another voice of your choosing. Then, make a dropdown to let the _user_ decide which voice to use!

## More
These are some of the options available, but it's up to you to make whatever you'd like. Take these tools and create something fun!
