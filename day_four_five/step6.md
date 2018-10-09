# Displaying a single Post

We now have a list of Posts rendered using data from the internet. It would be cool if we could now click on one of the posts, and navigate to a dedicated page for the selected post.

Your challenge in this step is to do just that.

The posts API allows us to get an individual post by it's `id` property by making a `GET` request to `/posts/{id}`

Create a new file `post.html` in the project root directory. In this file, make a request to get the data for the post with an `id` of `1`, and use the resulting data to render a single `Post` component to the DOM.

The resulting code should look very similar to your `index.html` file.

<details>
  <summary>Spoiler</summary>
  ```html
...
<body>
  <div id="root"></div>
  <script src="components/Post.js"></script>
  <script src="lib/DOM.js"></script>
  <script src="lib/DataSource.js"></script>
  <script>
    const dom = new DOM('#root');
    const dataSource = new DataSource('https://jsonplaceholder.typicode.com');

    dataSource.get('/posts/1', function (post) {
      dom.render(Post(post));
    });
  </script>
</body>
...
  ```
</details>  


### Navigating to the new page
Once you've made the page, update your `Post` component, so that the post title (the `h3` tag) acts as a link to `page.html`.

#### Try it out
Open your index.html page and click on one of the new links - you should now be taken to the new page, and see the details just for the first post.

The next problem we have to solve is that no matter which link we click on, we are always shown the same post, not te one we clcked on.

This is because we are always making a request for `posts/1`. We need to update this code so that the request is made for the correct post id, not just `1` every time.

To do this, we can utilize the URL.

* [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)
