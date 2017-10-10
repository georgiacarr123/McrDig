:twisted_rightwards_arrows: **Driver and Navigator switch roles if you haven't already done so**

Firstly, do a `git pull <partnerName> master` so you have your partner's changes.

Displaying groceries
------
We now have an array of `groceries` which we can add string elements to using a form. Now we need to update our document (page) every time that array changes (every time a user submits the form).

We need to use JavaScript to manipulate our document. In order to do so we have to create an element that JavaScript can push content into.

1) In your `body` above the opening `form` tag add opening and closing `ul` tags, and give the opening tag an `id` attribute with a value of `groceries`.

2) Below the `addGrocery` function, define a new function called `updateGroceries`.

```javascript
function updateGroceries () {

}
```

3) Then assign our `#groceries` element to a variable `groceriesElement`:

```js
function updateGroceries () {
  var groceriesElement = document.querySelector('#groceries')
}
```

4) Then clear the element's contents:

```js
function updateGroceries () {
  var groceriesElement = document.querySelector('#groceries')
  groceriesElement.innerHTML = ''
}
```

5) Then create a `for` loop that goes through every element inside the `groceries` array and assigns the current  element's index to `currentIndex`:

```javascript
function updateGroceries () {
  var groceriesElement = document.querySelector('#groceries')
  groceriesElement.innerHTML = ''

  for (var currentIndex = 0; currentIndex < groceries.length; currentIndex++) {

  }
}
```

6) Now we want to find the current element in the array that we are iterating over. We can do so using bracket notation - passing the `currentIndex` variable into `groceries`. We'll then assign it to a new variable `grocery`.

```javascript
function updateGroceries () {
  var groceriesElement = document.querySelector('#groceries')
  groceriesElement.innerHTML = ''

  for (var currentIndex = 0; currentIndex < groceries.length; currentIndex++) {
    var grocery = groceries[currentIndex]
  }
}
```

7) Lastly, whilst still inside the `for` block, we want to append `grocery` to our `ul` which we gave an `id` of `groceries`. We do that as follows:

```javascript
function updateGroceries () {
  var groceriesElement = document.querySelector('#groceries')
  groceriesElement.innerHTML = ''

  for (var currentIndex = 0; currentIndex < groceries.length; currentIndex++) {
    var grocery = groceries[currentIndex]

    groceriesElement.innerHTML += '<li>' + grocery + '</li>'
  }
}
``` 

***
:bulb:

`innerHTML` refers to the enclosed contents in an opening/closing pair of tags. `+=` says take the string we already have and append this string to the right to it. `'<li>' + grocery + '</li>'` is string concatenation - we're using + to append 3 different strings together.
***

8) Now all that's left to do is to call our `updateGroceries` function inside the `addGrocery` function. Remove the `console.log` (you don't need it now) and put `updateGroceries()` in its place. Give it a go in the browser.

9) Add, commit and push.

Complete code
------
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Shopping List</title>
</head>
<body>
  <ul id="groceries">
  </ul>

  <form id="addGroceryForm" method="post">
    <input id="groceryInput" type="text" placeholder="New grocery">
    <button type="submit">Add</button>
  </form>

  <script type="text/javascript">
    var groceries = []
    document.querySelector('#addGroceryForm').addEventListener('submit', addGrocery)


    function addGrocery (event) {
      event.preventDefault()

      var groceryInput = document.querySelector('#groceryInput')
      groceries.push(groceryInput.value)
      groceryInput.value = ''

      updateGroceries()
    }

    function updateGroceries () {
      var groceriesElement = document.querySelector('#groceries')
      groceriesElement.innerHTML = ''
      
      for (var currentIndex = 0; currentIndex < groceries.length; currentIndex++) {
        var grocery = groceries[currentIndex]
        groceriesElement.innerHTML += '<li>' + grocery + '</li>'
      }
    }
  </script>
</body>
</html>
```