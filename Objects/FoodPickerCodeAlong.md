# Code-Along: Food Picker
In this code-along, create a website to help visitors decide which food they should eat!

## Setting Up
[Click here to go to the Food Picker Start project.](https://hytop.onrender.com/e/food-picker-start)

1. Copy the project
1. Run the project
1. Click the "Get Food" button
1. Realize that nothing is happening
1. Panic
1. Realize that these instructions will show how to make the button work
1. Feel a wave of relief wash over you

## Hooking Up the Button
The first step is to add basic functionality to the button.

1. Open the **index.html** file
1. Notice the `<button>` has an `onclick` that calls the `getFood` function
    - But it has yet to be defined!
1. Open the **script.js** file for editing
1. Scroll down to the "Add New Code Below" comment
1. Make a new line under the comment
1. Define a function named `getFood`
1. In the body of the function, add an `alert` that says "Calculating"

Run the project again, click the button, and verify that the pop-up message appears! The code should look something like this:

```js
function getFood() {
  alert("Calculating...");
}
```

## Getting a Random Item
Next, find a random item. There are a few things to notice in the existing code:

- The `items` array contains various food objects, that all contain some properties
- The `getRandomInt` function will return a random integer between `0` and the `max`

The code will have to find a random item using the existing code.

1. Make a new line in the body of the `getFood` function
1. Create a new variable named `randomItemIndex`
1. Set `randomItemIndex` to be a call to `getRandomInt`
1. Pass in `items.length` to the `getRandomInt` call
1. Under that, create a new variable named `item`
1. Set `item` to be the value from the `items` array at the `randomItemIndex` index

The code should look something like this:

```js
  let randomItemIndex = getRandomInt(items.length);
  let item = items[randomItemIndex];
```

This will not change the functionality of the button yet, but now we have a random item!

## Displaying the Random Item Name
Now it is time to display the item information.

1. Open the **index.html** file
1. Notice there is a `<p>` element with an `id` of `food-name`
    - This can store the name of the random food item!
1. Open the **script.js** file for editing
1. Make a new line in the body of the `getFood` function
1. Create a new variable named `foodNameElement`
1. Set `foodNameElement` to select the `<p id="food-name">` element
    - Using `document.querySelector`
1. Under that, create a new variable named `foodNameText`
1. Set `foodNameText` to be `ITEM (STORE)`
1. Make the string into a template literal
1. In the literal, replace `ITEM` with `${item.name}`
    - This gets the `name` property of the `item` object
1. In the literal, replace `STORE` with `{$item.store}`
    - This gets the `store` property of the `item` object
1. Set the `textContent` property of `foodNameElement` to `foodNameText`
    - This sets the actual element text so it will appear on the page

Run the project, click the button, and verify that a random food item name is properly displayed! The additional code should look something like this:

```js
let foodNameElement = document.querySelector("#food-name");
let foodNameText = `${item.name} (${item.store})`;
foodNameElement.textContent = foodNameText;
```

## Displaying the Random Item Picture
The name is good, but it would be much more appetizing with a picture. Luckily, there are some pictures accessible via URL.

1. Open the **index.html** file
1. Notice there is a `<p>` element with an `id` of `food-pic`
    - This can store the name of the random item picture!
1. Open the **script.js** file for editing
1. Make a new line in the body of the `getFood` function
1. Create a new variable named `foodPictureElement`
1. Set `foodPictureElement` to select the `<p id="food-pic">` element
    - Using `document.querySelector`
1. Under that, create a new variable named `foodPictureUrl`
1. Set `foodPictureUrl` to be `https://raw.githubusercontent.com/hytechclub/web-103/main/Assets/URL`
1. Make the string into a template literal
1. In the literal, replace `URL` with `${item.picture}`
    - This gets the `picture` property of the `item` object
1. Set the `src` property of `foodPictureElement` to `foodPictureUrl`
    - This sets the actual image URL so that it displays on the page

Run the project, click the button, and verify that a random food item picture is properly displayed! The additional code should look something like this:

```js
let foodPictureElement = document.querySelector("#food-pic");
let foodPictureUrl = `https://raw.githubusercontent.com/hytechclub/web-103/main/Assets/${item.picture}`;
foodPictureElement.src = foodPictureUrl;
```

## Creating a Greek Salad Object
The page should now be fully functional! All that's left is adding some additional food items. Start by creating a new object for a greek salad from Panera.

1. Make a new line at the bottom of the **script.js** file
    - Make sure it's outside of the `getFood` function (after the `}`)
1. There, create a new variable named `greekSalad`
1. Set `greekSalad` to be a new empty object with `{` and `}`
    - Press **Enter** to automatically add space between
1. In the object, create a `store` property set to `"Panera"`
    - Property name, colon, property value, comma
1. Under that in the object, create two more properties:  
    - `price` set to `10`
    - `picture` set to `greeksalad.jpg`

The new code should look something like this:

```js
let greekSalad = {
  store: "Panera",
  price: 10,
  picture: "greeksalad.jpg"
};
```

It will not change the functionality of the site yet - the item must be added to the `items` array!

## Adding the Greek Salad Object
Now the `greekSalad` is almost ready, but there are a couple things still needed before it will show up as a food item.

1. Make a new line at the bottom of the **script.js** file
1. There, set the `name` property of the `greekSalad` object to be `"Greek Salad"`
    - This ensures that it has a name for the display!
1. Under that, push the `greekSalad` object to the `items` array

At this point:

- The `name` property has been added to the `greekSalad` object
- The `greekSalad` object has been added to the `items` array

Run the project, click the button a few times, and verify that the Greek Salad eventually appears! Note that it may be helpful to remove the `alert` statement from the top of the `getFood` function for usability purposes. The site also runs slowly sometimes, so if the image is not changing, it may be necessary to wait several seconds.

The additional code should look something like this:

```js
greekSalad.name = "Greek Salad";
items.push(greekSalad);
```

## Creating and Adding a Mac n Cheese Object
Now it will be possible to add new items in a few different ways! Add a Mac n Cheese item to the menu.

1. Make a new line at the bottom of the **script.js** file
1. There, create a new variable named `mac`
1. Set `mac` to be a new empty object with `{` and `}`
    - Press **Enter** to automatically add space between
1. In the object, create a `store` property set to `"Panera"`
    - Property name, colon, property value, comma
1. Under that in the object, create a `name` property set to `"Mac n Cheese"`
1. Under that in the object, create a `price` property set to `7`
1. Under that in the object, create a `picture` property set to `"macncheese.jfif"`
    - Note that there is a file with the URL `https://raw.githubusercontent.com/hytechclub/web-103/main/Assets/macncheese.jfif` 
1. Under that, _outside_ the object (after `}`), make a new line
1. There, push the `mac` object to the `items` array

Run the project, click the button a few times, and verify that the Mac n Cheese eventually appears! The additional code should look something like this:

```js
let mac = {
  store: "Panera",
  name: "Mac n Cheese",
  price: 7,
  picture: "macncheese.jfif"
};

items.push(mac);
```

## Creating and Adding a Soup Object
It is also possible to add a new item directly without creating a separate variable! Add Soup to the possible Panera food items in this manner.

1. Make a new line at the bottom of the **script.js** file
1. Push a currently empty object to the `items` array
1. Add a `store` property to the pushed object set to `"Panera"`
1. Add a `name` property to the pushed object set to `"Soup"`
1. Add a `price` property to the pushed object set to `6`
1. Add a `picture` property to the pushed object set to `"panerabread.jpg"`

Run the project, click the button a few times, and verify that the Soup eventually appears! The additional code should look something like this:

```js
items.push({
  name: "Soup",
  price: 6,
  picture: "panerabread.jpg"
});
```

## Conclusion
That's it for the code-along activity! At this point, it should be possible to click the button, and see a variety of different foods appear.

The added code in the **script.js** file should look something like this:

```js
function getFood() {
  let randomItemIndex = getRandomInt(items.length);
  let item = items[randomItemIndex];

  let foodNameElement = document.querySelector("#food-name");
  let foodNameText = `${item.name} (${item.store})`;
  foodNameElement.textContent = foodNameText;

  let foodPictureElement = document.querySelector("#food-pic");
  let foodPictureUrl = `https://raw.githubusercontent.com/hytechclub/web-103/main/Assets/${item.picture}`;
  foodPictureElement.src = foodPictureUrl;
}

let greekSalad = {
  store: "Panera",
  price: 10,
  picture: "greeksalad.jpg"
};

greekSalad.name = "Greek Salad";
items.push(greekSalad);

let mac = {
  store: "Panera",
  name: "Mac n Cheese",
  price: 7,
  picture: "macncheese.jfif"
};

items.push(mac);

items.push({
  store: "Panera",
  name: "Soup",
  price: 6,
  picture: "panerabread.jpg"
});
```

## Next Steps
[Click here to view the self-paced work instructions.](SelfPacedWork.md)
