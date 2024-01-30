# Self-Paced Work
Follow these instructions to update the Food Picker website.

## New Items
Feel free to add any new items desired! At minimum, add one new item for each existing restaurant:

| Restaurant | Item Name | Price | Picture |
|-|-|-|-|
| McDonald's | McPlant | 10.99 | mcplant.jpg |
| Chipotle | Chips | 5.00 | chips.png |
| Taco Bell | Cheesy Roll Up | 1.00 | cheesyroll.jpg |
| Panera | Bagel | 4.50 | bagel.jpg |

Feel free to add these items directly when the `items` array is created, or add them in the way the Panera items were added. Whatever works!

Make sure it is possible to click the button and see all items appear.

## New Restaurant: Arby's
Next, add an entirely new restaurant. This can be done in the same way that Panera was added, or added wholesale to the `items` array.

#### Store
Arby's

#### Items
| Item Name | Price | Picture |
|-|-|-|
| Combo | 2.99 | combo.jpg |
| Curly Fries | 4.09 | curlyfries.png |
| Roast Beef | 2.00 | roastbeef.jpg |

## Price Display
There is a `price` property stored with every object in the `items` array, but it is currently not being used at all! Display a price along with each item name and picture.

### HTML: Price Paragraph
Add a new `<p></p>` element to the page to store the price.

1. Open the **index.html** file for editing
1. Find the `<p id="food-name"></p>`
1. Make a new line, and create a new `<p></p>` element
1. Set the `id` of the new `<p>` to be `food-price`

Now the HTMl should be ready to go...

### JavaScript: Setting the Food Price
Next, update the value of the `<p id="food-price>` element with the proper price.

1. Open the **script.js** file for editing
1. Make a new line at the bottom of the `getFood` function body
1. There, create a new variable named `foodPriceElement`
1. Set `foodPriceElement` to select the `<p id="food-price">` element
    - Using `document.querySelector`
1. Under that, create a new variable named `foodPriceText`
1. Set `foodPriceText` to be `Price: $PRICE`
1. Make the string into a template literal
1. In the literal, replace `PRICE` with `${item.price}`
    - This gets the `price` property of the `item` object
    - Make sure to keep the original "$" in front of the price
1. Set the `textContent` property of `foodPriceElement` to `foodPriceText`
    - This sets the actual element text so it will appear on the page

At this point, run the project, click the button, and verify that the proper prices appear!

## Always New
Currently, when generating a random food item, it is possible to choose the same item. Fix this issue so that there is a brand new item every time someone clicks the "Get Food" button.

1. Open the **script.js** file for editing
1. Find the `foodNameText` variable creation
1. Under that, create an `if` statement
1. For the conditional, check if `foodNameText` is equal to `foodNameElement.textContent`
1. In the body of the `if`, call the `getFood` function
1. Under that, still in the body, `return` from the function

Run the project, click the button a few times, and verify that there is always a new item!

## CHALLENGE: Restaurant Filter
Currently, the button selects a random restaurant and then a random item. Instead of doing this, ask the user which restaurant they would like to visit, and then choose randomly from that restaurant's items.

### HTML: Restaurant Name Input Element
Start by creating a new element in the HTML where the user can enter a restaurant name.

1. Open the **index.html** file for editing
1. Find the opening `<p></p>` element with the welcome message
1. Make a new line under that, and create a new `<p></p>` element
1. Set the text to say "Enter a restaurant: "
1. After that, within the `<p>` and `</p>`, create an `<input>` element
1. Set the `id` of the `<input>` to be `"restaurant"`

Run the project and verify that the text box appears on the page.

### JavaScript: Getting the Restaurant Name
Next, select the new `<input id="restaurant">` element, and get its value.

1. Open the **script.js** file for editing
1. Make a new line at the _top_ of the `getFood` function
1. There, create a new variable named `restaurantNameInput`
1. Set `restaurantNameInput` to select the `<input id="restaurant">` element
    - Using `document.querySelector`
1. Under that, create a new variable named `restaurantName`
1. Set `restaurantName` to be the `value` of the `restaurantNameInput` variable

Now the name is ready to go.

### JavaScript: Finding the Items for the Restaurant
Once the name has been retrieved, it will be possible to use it to find the proper object for the restaurant.

1. Under the `restaurantName` variable, make a couple new lines in the `getFood` function
1. There, create a new variable named `restaurantItems` set to an empty array `[]`
1. Next, create a `for` loop to loop through each element in the `items` array
    - `for`
    - Parentheses
    - Curly Brackets
    - Initialization (`let i = 0`)
    - Condition (`i < items.length`)
    - Increment (`i++`)
1. In the body of the `for` loop, create an `if` statement
    - `if`
    - Parentheses
    - Curly Brackets
1. For the condition, check if `items[i].store` is equal to `restaurantName`
    - This means the current index has an item from the given restaurant
1. In the body of the `if`, `push` the `items[i]` object to the `restaurantItems` array
    
Now the `restaurantItems` variable should be ready to go! Replace the `items` references in the code below with `restaurantItems` to ensure that only items from the given restaurant are available.

Run the project, enter a restaurant name, and click the button. It should only choose food items from that restaurant! It's not perfect, though...

### JavaScript: Dealing with Unfound Restaurants
Currently, when entering a restaurant name that is not found, the page should fail. Fix this by handling unfound restaurants.

1. Under the `for` loop, create an `if` statement
    - `if`
    - Parentheses
    - Curly Brackets
1. Set the condition to check if `restaurantItems.length` is `0`
1. In the body of the `if`, copy the old code that found a random restaurant

Run the project, enter a name that does not exist, and verify that it chooses randomly from all restaurant items!

## CHALLENGE: Vegetarian Filter
There may be some vegetarians who visit the site - these people would not like to see any items that contain meat. Update the code so they can select only vegetarian items!

### HTML: Vegetarian Only Checkbox
Start by creating a new element in the HTML where the user can check whether they'd like only vegetarian items.

1. Open the **index.html** file for editing
1. Find the `<p></p>` element with the restaurant name `<input>`
1. Make a new line under that, and create a new `<p></p>` element
1. Set the text to say "Vegetarian items only? "
1. After that, within the `<p>` and `</p>`, create an `<input>` element
1. Set the `type` of the `<input>` to be `"checkbox"`
1. Set the `id` of the `<input>` to be `"veg"`

Run the project and verify that the checkbox appears on the page.

### JavaScript: Getting the Checkbox Value
Now the checkbox is there, but its value must be retrieved.

1. Open the **script.js** file for editing
1. Find the `restaurantItems` variable declaration
1. Make a new line _above_ the variable
1. There, create a new variable named `vegetarianCheckbox`
1. Set `vegetarianCheckbox` to select the `<input id="veg">` element
    - Using `document.querySelector`
1. Under that, create a new variable named `vegOnly`
1. Set `vegOnly` to be the `checked` property of the `vegetarianCheckbox` variable

Now the function knows if non-vegetarian items should be filtered out, but it still does not know which items are vegetarian!

### JavaScript: Vegetarian Property
Currently, the item objects do not have a property denoting which items are vegetarian.

Go through each item object, within the `restaurants` variable and manually add a `veg` property - it should be set to `true` of the item can be vegetarian, and `false` if the item contains meat.

### JavaScript: Filtering the List
There is a very helpful [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) function that makes it possible to filter arrays based on functions that return booleans. Passing functions as variables and using arrow function syntax are concepts that will be covered later in this course. For now, try to figure out how to use `filter` even if you don't fully understand it!

1. Under the `restaurantItems` variable in the `getFood` function, make a new line
1. There, create an `if` statement
1. For the condition, check if `vegOnly` is true
1. In the body, set the `restaurantItems` variable to a call to `restaurantItems.filter`
1. For the `filter` call, pass in a function checking if an `item` has a `veg` property set to `true`
    - `item => item.veg`

Run the project, check the box, and verify that only vegetarian items appear!
