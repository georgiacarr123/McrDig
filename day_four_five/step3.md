# Post Component

For this application, any HTML rendered to the DOM by JavaScript will be encapsulated inside its own function for re-usability. We will call these functions _components_.

When we make a GET request to `/posts` through our `DataSource` object, we get back an array of objects. Each object looks like this:

```js
{
  id: 102,
  userId: 1,
  title: "my post",
  body: "woooo"
}
```

The `Post` component needs to take this data and output it to HTML. For this project, it's recommended you create a `components` folder in your project root folder, and give each component it's own `.js` file.

Here's a start on `Post.js`:

```js
function Post (post) {
  return `
    <div>
      <a href="post.html?id=${post.id}"><h3>${post.title}<h3></a>
    </div>
  `;
}
```

It will become clearer in later steps why we've linked to `post.html?id=${post.id}` so don't worry too much about it now.

If you're observant, you'll notice that the post `body` isn't outputted above. Go ahead and add it now.

## Try it out

In your `index.html` file, include in the component file. Inside your `DOM` instance's `render` method (create a new instance if you deleted your practice code from earlier), call the `Post` component function, passing in the following object:

```js
{
  id: 102,
  userId: 1,
  title: "my post",
  body: "woooo"
}
```

<details>
  <summary>Spoiler</summary>

  ```js
  const post = {
    id: 102,
    userId: 1,
    title: "my post",
    body: "woooo"
  };

  dom.render(Post(post));
  ```

</details>

You should see the post outputted to your `div#root` element.

## [Step 4: Posts Component](step4.md)
