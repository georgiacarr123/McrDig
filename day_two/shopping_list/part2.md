:twisted_rightwards_arrows: **Driver and Navigator switch roles if you haven't already done so**

Partner pulls
------
Again, the person who is now driving will need to pull their partner's changes. They to will need to add their partner's GitHub repo as a *remote* and pull down:

```
git remote add <partnersName> https://github.com/<username>/shoppingList
git pull <partnersName> master
```

Handling the form input
------
When a user submits the form, we want to add the contents (or the current *value*) of the text input to an array of groceries.

1) Inside the `script` tags, define a new variable called `groceries` and assign the variable an empty array (`[]`). 

```javascript
var groceries = []
```

2) Then add an event listener to `#addGroceryForm` for a submit action. We want to call the `addGrocery` function when this event is fired:

```js
document.querySelector('#addGroceryForm').addEventListener('submit', addGrocery)
```

3) Now create the function `addGrocery`. Give it a parameter of `event` as our `addEventListener` method above will give us an `event` argument which is an object containing information about the event.

```javascript
function addGrocery (event) {

}
```

4) Inside the function, call `preventDefault` on the `event` object. This will stop the default action of the event - in this case it will stop the form from reloading the page:

```js
event.preventDefault()
```

3) Still inside the function block, define a new variable called `groceryInput` and assign it `document.querySelector('#groceryInput')`.

```javascript
function addGrocery (event) {
  event.preventDefault()

  var groceryInput = document.querySelector('#groceryInput')
}
```

4) Then call `.push` on the `groceries` array, and pass in `groceryInput.value` as an argument:

```js
function addGrocery (event) {
  event.preventDefault()

  var groceryInput = document.querySelector('#groceryInput')
  groceries.push(groceryInput.value)
}
```

5) Next, we'll clear the value of the `#groceryInput` field, by setting its value to an empty string:

```js
function addGrocery (event) {
  event.preventDefault()

  var groceryInput = document.querySelector('#groceryInput')
  groceries.push(groceryInput.value)
  groceryInput.value = ''
}
```

***
:bulb:

You may notice we've called `.value` on `document.querySelector('#groceryInput')`. This gets us the `value` attribute of the found element.
***

6) To finish this function off, add another line with `console.log(groceries)` (so we can check in our browser console that the array is being updated).

```js
function addGrocery (event) {
  event.preventDefault()

  var groceryInput = document.querySelector('#groceryInput')
  groceries.push(groceryInput.value)
  groceryInput.value = ''

  console.log(groceries)
}
```

7) Save the file and open in your browser. Try adding items to the form. You should see the array update in your browser console.

8) Add, commit to *local* and push changes to *remote*:

```bash
git add index.html
git commit -m "add grocery to array on form submit"
git push
```

:twisted_rightwards_arrows: **Driver and Navigator switch roles**

[Next: Displaying Array Items](part3.md)