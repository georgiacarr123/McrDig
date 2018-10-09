# Post Component

We can now render ay HTML string to the DOM by passing it into our `dom.render` method. 

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

The `Post` component needs to take this data and output some HTML that incorporates the data. For this project, it's recommended you create a `components` folder in your project root folder, and give each component it's own `.js` file.

Here's a start on `Post.js`:

```js
function Post (post) {
  return `
    <div>
      <h3>${post.title}<h3>
    </div>
  `;
}
```

If you're observant, you'll notice we are only using the posts `title`, but not the `id` or `body`.

Add the following features to the `Post` component:

1. Display the post data's `body` text below the title.
2. Add an `id` to the `<div>` tag, setting its value to `post-${post.id}`

## Try it out

In your `index.html` file, include in the component file. 

The index.html file should currently contain something like this:


```js
const dom = new DOM('#root');
dom.render('<h1>Hello World</h1>');
```

We have now built a `Post` component, a function that returns a HTML string. Update your code and pass the `Post` function into the `DOM` instance's `render` method. The `Post` component expects some post data, so call the `Post` component function, passing in the following object:

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
