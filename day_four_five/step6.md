# Displaying a single Post

We now have a list of Posts rendered using data from the internet. It would be cool if we could now click on one of the posts, and navigate to a dedicated page for the selected post.

Your challenge in this step is to do just that.

The posts API allows us to get an individual post by it's `id` property by making a `GET` request to `/posts/{id}`

Create a new file `post.html` in the project root directory. In this file, make a request to get the data for the post with an `id` of `1`, and use the resulting data to render a single `Post` component to the DOM.

The resulting code should look very similar to your `index.html` file.


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
