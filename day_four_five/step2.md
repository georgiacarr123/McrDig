# DOM

You will create a DOM constructor and prototype, which will act as a wrapper around [Element.innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML).

## Getting started

Inside `lib`, create a `DOM.js` file.

## DOM constructor

`DOM` will be instantiated with a CSS selector, which will be used to find a HTML element (and later replace its contents):

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
