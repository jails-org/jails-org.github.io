# innerHTML 
``` ( html:string ) => void ```
> An innerHTML function to update a HTMLElement with string with dom diffing.

In practice that's the same idea of using `elm.innerHTML` and send a HTML string to your component. The difference here is that `innerHTML` interface uses `morphdom` in order to make optimal changes into the dom.

This is specially usefull if you are working with a server-side driven model, just like you would do with `htmx`, where your server sends `html` over the ajax calls instead a JSON api.

---

```js
import jails from 'jails-js'
import * as mycomponent from 'components/my-component'

jails.register('my-component', mycomponent)
```

*components/my-component.js*

```js
export default function mycomponent ({ main, on, innerHTML }) {

    let count = 1

    main( _ => {
        on('click', button, updateElement)
    })

    const updateElement = () => {
        innerHTML(`
            <h1>Hello World - Counter ${count++}<h1>
        `)
    }
}
```