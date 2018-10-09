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

To do this, we can utilize the URL, in particular by utilizing a **query string** (also known as a search parameter). This is the part of the url starting with a `?`. It's formatted as a set of key-value pairs in the format `?key=value`.

If you go to Google and perform a search (search for "ducks"), you will see that the main URL is `https://www.google.co.uk/search`, and this is followed by some query string params (including `q=ducks`). Each param is separated by an `&`.

We can access and use these params in our JavaScript code to add extra flexibility to our page.

Firstly, update the link URL in your `Post` component from `page.html` to `page.html?id=${post.id}`.

When you click on the link now, you should see the correct ID for the post appearing in the browser address bar. Now we need to use this.

The next thing we need to do is, in the `post.html` page, grab this `id` parameter value from the URL, and update our `GET` request to request the data for this post, instead of the one with an id of `1`.

You can get information about the current URL using the `window.location` object. Take a look at this object, and see if you can find the information we need.

You can parse this query string into a JavaScript object using `URLSearchParams`, which has a number of methods for interacting with a query string.

### Resources
* [`window.location`](https://developer.mozilla.org/en-US/docs/Web/API/Location)
* [Anatomy of a URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL)
* [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)

<details>
  <summary>Spoiler</summary>

```html
  <script>
    const dom = new DOM('#root');
    const dataSource = new DataSource('https://jsonplaceholder.typicode.com');
    
    const searchParams = new URLSearchParams(window.location.search);
    const postId = searchParams.get('id');

    dataSource.get(`/posts/${postId}`, function (post) {
      dom.render(Post(post));
    });
  </script>
  ```

</details>  

Once you have done this, you should see the correct data being loaded when you navigate to the `post.html` page.

## [Step 7: Displaying Comments](step7.md)
