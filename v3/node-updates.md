
# Node Updates

> If you wonder why in some cases the dom updates behaves unexpectedly, maybe it might be related to the fact that you're updating DOM manually, without using `reactor` to update the state.

You can bypass dom diffing using `data-static` property, `reactor` will notice that attribute and bypass virtual dom changes on the specific node.

!> Its also usual to use `data-static` property in form elements like : `input`, `textarea`, `select` etc, in order to let the browser persists value instead of having to handle the values yourself using some `value` state.

### The Lazyload Image case

```html
<div data-component="my-component">
    ...
    <p>...</p>
    <img data-src="/some/path/image.jpg" alt="My Lazyload Image" />
</div>
```

In the example above, we have an image that will be lazyloaded, so in another part of our application, there's a script that will execute on page load, scanning all images that has `data-src` preload them and then it will change image attribute to `src` :

```html
<img src="/some/path/image.jpg" alt="My Lazyload Image" />
```

It will work as long you don't update `my-component` using `reactor()` calls. That's because reactor will register template in the page load, and will be using only that template version on future updates using the new state passed. If you change the DOM manually, reactor will update that image to the initial version:

```html
<img data-src="/some/path/image.jpg" alt="My Lazyload Image" />
```

In order to solve that, you can use `data-static` to bypass any dom diffing and preserve a specific node and its descendents to its original and static version and prevent them to be updated on `reactor` calls.

```html
<img data-src="/some/path/image.jpg" alt="My Lazyload Image" data-static />
```
---