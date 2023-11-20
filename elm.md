# elm
``` elm: HTMLElement ```
> A reference to the current html element.

This property is a reference to the current `HTMLElement` so you can work with DOM api without having to query it using `querySelector` and, more importantly, it will help you to avoid to query an element that is outside the component scope as you would do in Vanilla Javascript.

---

*index.html*

```html
<my-component>
    ...
</my-component>
```

*main.js*

```js
import jails from 'jails-js'
import * as mycomponent from 'components/my-component'

jails.register('my-component', mycomponent)
```

*components/my-component.js*

```js
export default function mycomponent ({ main, elm }) {

    main( _ => {
        console.log(`Hi! I'm`, elm) 
        // Hi! I'm <my-component...>
    })
}
```