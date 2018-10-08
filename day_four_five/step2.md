# DOM

You will create a DOM constructor and prototype, which will act as a wrapper around [Element.innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML).

## Getting started

Inside `lib`, create a `DOM.js` file.

## DOM constructor

`DOM` will be instantiated with a CSS selector, which will be used to find a HTML element (and later replace its contents). Here's an example of its instantiation:

HTML:

```html
<div id="root"></div>
```

JS:

```js
const dom = new DOM('#root');
```

Using the above as a guide, go ahead and create the constructor. It should set an internal (private) property called `_rootElement` to the JS DOM element that matches the passed CSS selector (you'll need to use [document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelector)).

<details>
  <summary>Hint:</summary>

  ```js
  this._rootElement = document.querySelector(rootElement);
  ```

</details>

## DOM.prototype.render()

`DOM.prototype.render()` will be responsible for rendering HTML to the `_rootElement`, overriding any existing contents between it's opening and closing tags.

An example of its usage:

```js
const dom = new DOM('#root');
dom.render('<h1>Hello World</h1>');
```

Would change:

```html
<div id="root"></div>
```

To:

```html
<div id="root"><h1>Hello World</h1></div>
```

You should be able to achieve this on your own, but please ask for help if you get stuck. Remember, you have access to the `div#root` element on your `DOM` instance via the `_rootElement` property, and you can use [Element.innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) to change its contents.

***
:innocent: You should now try this out. In your `index.html` file, add a `div` to your HTML and give it a unique `id`. Instantiate your `DOM` object, and use the `render` method on the instance to replace the contents of your div (nothing) with `<h1>Hello World</h1>`.
***
