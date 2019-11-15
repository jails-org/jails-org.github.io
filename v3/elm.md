# Elm

> A reference to a `HTMLElement`.

When you register a Jails component, you need to specify where it gonna mount, for every component there's a `elm` variable pointing to the `HTMLElement` registered. You should use it to scope your `querySelector` calls and avoid at any cost leaking `DOM` queries.

---

*index.html*

```html
<section data-component="my-component">
    ...
</section>
```

*main.js*

```js
import jails from 'jails-js'
import * as mycomponent from 'components/my-component'

jails.register('my-component', mycomponent)
```

*components/my-component.js*

```js

export default ({ main, elm }) => {

    main(() => [
        whoami
    ])

    const whoami = () => {
        console.log(`Hi! I'm`, elm) // Hi! I'm <section data-component="my-component"...>
    }
}
```