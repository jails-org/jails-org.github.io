# unmount
``` ( fn:Function ) => void ```
> An unmount function to destroy/kill references and bindings.

A function that takes a callback that will be executed when the `HTMLElement` of that component is deatached from DOM. You can use this function to unsubscribe or unregister your component and prevent memory leaks or multiple bindings.

---

```js
import jails from 'jails-js'
import * as mycomponent from 'components/my-component'

jails.register('my-component', mycomponent)
```

*components/my-component.js*

```js
export default function mycomponent ({ main, elm, unmount }) {

    main( _ => [
        
    ])

    unmount(() => {
        console.log('I was removed from DOM! =X')
    })
}
```