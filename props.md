# .props

> The props handler gets all the html attributes of the component `HTMLElement`, such as : `id`, `class`, `style`, `data` etc.

The main difference between calling `props()` and `.getAttribute()` is that getAttribute method will always return a `string` and `props` parses the value to the right type.

```html
<div data-component="user" id="my-user" data-options="{name:'Clark Kent', age :33}">
    <!-- ... -->
</div>
```

```js
export default ({ main, elm, props }) => {

    const {options} = props('data') // Almost the same as elm.getAttribute('data-options')
    const id = props('id') // The same as elm.getAttribute('id') or elm.id

    main(() => [
        //...
    ])
}
```

