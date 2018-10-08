# Displaying a single Post

Code:

```js
const dom = new DOM('#root');
const dataSource = new DataSource('https://jsonplaceholder.typicode.com');
const queryParams = new URLSearchParams(window.location.search);
const postId = queryParams.get('id');
dataSource.get(`/posts/${postId}`, function (post) {
  dom.render(Post(post));
})
```

* [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)
