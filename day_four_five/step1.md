# DataSource

You will create a DataSource constructor and prototype, which will act as a wrapper around XMLHttpRequest.

## Getting started

Using the command line/Terminal:

1. Create a new project folder `reddit-clone`. 
2. `cd` into `reddit-clone`.
3. Make a `lib` folder.
4. Inside `lib`, create a `DataSource.js` file.

## DataSource constructor

`DataSource` will be instantiated with a base API URL e.g.:

```js
const dataSource = new DataSource('https://jsonplaceholder.typicode.com');
```

Using the above as a guide, go ahead and create the constructor. It should set an internal (private) property called `_baseUrl` to the URL passed as an argument.

## DataSource.prototype.get()

You want to be able to make a GET request with a `DataSource` instance by calling its `get` method e.g.:

```js
const dataSource = new DataSource('https://jsonplaceholder.typicode.com');

dataSource.get('/posts', function (posts) {
  console.log(posts); // [{ id: 1, title: 'post 1' }, { id: 2, title: 'post 2' }]
})
```

You can see that the `get` method will take 2 arguments. The first is an `endpoint` which will be appended within the method to the `_baseUrl` property set earlier to make the HTTP request. The second is a function which should be called once the request has finished - it is passed the response from the request. 

Steps to complete:

1. Create a new `get` method on your `DataSource.prototype`. It should accept the arguments mentioned above, so should have 2 parameters `endpoint` and `callback`.
2. Create a new instance of `XMLHttpRequest`, assigning it to a variable so you can call its methods/access its properties.
3. Call the [open](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/open) method on your `XMLHttpRequest` instance to specify details about the request you want to make. Pass in `GET` for the `method`. For the `url` you should concatenate your DataSource instance's `_baseUrl` property value to the `endpoint` parameter.
4. Call the [setRequestHeader](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/setRequestHeader) method on your `XMLHttpRequest` instance to tell the API you're asking for data to send it back in JSON format. Pass `Content-Type` as the first argument, and `application/json;charset=UTF-8` as the second.
5. Overwrite the `onreadystatechange` property of your `XMLHttpRequest` instance, assigning it a function.
6. Inside the function, write an `if` statement that checks if the [readyState](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/readyState) property of your `XMLHttpRequest` is `4` and that the [status](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/status) property is `200`.
7. If your `if` statement is true then call your `callback` function, passing in the value of your `XMLHttpRequest` instance's `response` property. You should use [JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse) to convert the returned JSON string to a JavaScript object.
8. Outside of your `onreadystatechange` method, call `send` on your `XMLHttpRequest` instance to perform the GET request.

<details>
  <summary>Spoiler: Code - Don't copy and paste!</summary>

  ```js
  get: function (endpoint, callback) { // 1
    const xhr = new XMLHttpRequest(); // 2
    
    xhr.open('GET', this._baseUrl + endpoint); // 3
    xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8"); // 4
    xhr.onreadystatechange = function () { // 5
      if (xhr.readyState === 4 && xhr.status === 200) { // 6
        callback(JSON.parse(xhr.response)); // 7
      }
    };

    xhr.send(); // 8
  }
  ```

</details>

***
:innocent: You should now try this out. Create an `index.html` file, include in your `DataSource.js` file, and have a go instantiating a new `DataSource` and making a `GET` request. Look at the examples above if you aren't sure.
***

## DataSource.prototype.post()

You want to be able to make a POST request with a `DataSource` instance by calling its `post` method e.g.:

```js
const dataSource = new DataSource('https://jsonplaceholder.typicode.com');
const newPost = {
  userId: 1,
  title: 'my post',
  body: 'woooo'
};

dataSource.post('/posts', newPost, function (createdPost) {
  console.log(createdPost); // { id: 101, userId: 1, title: 'my post', body: 'woo' }
})
```

You can see that the `get` method will take 3 arguments. The first is an `endpoint` which will be appended within the method to the `_baseUrl` property set earlier to make the HTTP request, same as with the `get` method. The second is the `data` you wish to send in your request, and the third is a `callback` function which should be called once the request has finished - it is passed the response from the request - in this case, the newly created object returned from the API. 

Steps to complete:

1. Create a new `post` method on your `DataSource.prototype`. It should accept the arguments mentioned above, so should have 3 parameters `endpoint`, `data` and `callback`.
2. Create a new instance of `XMLHttpRequest`, assigning it to a variable so you can call its methods/access its properties.
3. Call the `open` method on your `XMLHttpRequest` instance to specify details about the request you want to make. Pass in `POST` for the `method`. For the `url` you should concatenate your DataSource instance's `_baseUrl` property value to the `endpoint` parameter.
4. Call the `setRequestHeader` method on your `XMLHttpRequest` instance to tell the API you're asking for data to send it back in JSON format.
5. Overwrite the `onreadystatechange` property of your `XMLHttpRequest` instance, assigning it a function.
6. Inside the function, write an `if` statement that checks if the `readyState` property of your `XMLHttpRequest` is `4` and that the `status` property is `201` (`200` is `OK`, `201` is `Created`).
7. If your `if` statement is true then call your `callback` function, passing in the value of your `XMLHttpRequest` instance's `response` property. You should use `JSON.parse()` to convert the returned JSON string to a JavaScript object.
8. Outside of your `onreadystatechange` method, call `send` on your `XMLHttpRequest` instance to perform the POST request. You need to pass in the data to send as an argument, which will be your `data` objected converted to a JSON string using [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify).

<details>
  <summary>Spoiler: Code - Don't copy and paste!</summary>

  ```js
  post: function (endpoint, data, callback) {
    const xhr = new XMLHttpRequest();
    
    xhr.open('POST', this._baseUrl + endpoint);
    xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4 && xhr.status === 201) {
        callback(JSON.parse(xhr.response));
      }
    };

    xhr.send(JSON.stringify(data));
  }
  ```

</details>

***
:innocent: You should now try this out. In your `index.html` file, use your existing `DataSource` instance to make a POST request. Look at the examples above if you aren't sure.
***
