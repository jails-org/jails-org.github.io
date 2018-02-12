# Jails

## .start

Scans the document looking for `data-component` elements and apply a high-order function on that current element.
The `start` method expects a optional `context` as a parameter. When no `context` is provided, the scanner walks through the `document.documentElement` root.

The scanner will bypass a `HTMLElement` if it is already instantiated. Use this method to start your application and after update html when using `innerHTML`.

## .events

Events is an event helper that supports `Event Delegation` used by Jails and Components. Use it when you need to use `Event Delegation` and you are not using any library like `jQuery` to address that.

```js
const handler = () => {}

jails.events.on(document, 'click', handler)
jails.events.off(document, 'click', handler)
jails.events.trigger(document, 'click', {options:{}})

```

## .publish / .subscribe

It is a Pub/Sub helper also used in the Components. You can use pub/sub to make simple integrations between a third-party library and Jails components.

`main.js`

```js
import jails from 'jails-js'
import router from 'my-modules/router'

router('/:page', ( {page} )=>{
    jails.publish('page:change', page)
})
```

`components/my-component/index.js`
```js
export default ( {init:main} ) => {

    main(() => [
        start
    ])

    const start = ( {subscribe} ) =>
        subscribe('page:change', onPageChange)

    const onPageChange = page =>
        console.log( 'Page was changed', page )
}

```

## .destroy
Destroy events and references attached to a `HTMLElement` component node and fires a `:destroy` custom event.

```js
const mycomponent = document.body.querySelector('[data-component*=my-component]')
jails.destroy( mycomponent )
```

`my-component.js`
```js
export default ( {init:main} ) => {

    let interval = null

    main(() => [
        register,
        startInterval
    ])

    const register = ( {on} ) =>
        on(':destroy', killInterval)

    const startInterval = () =>
        interval = setInterval( () => {}, 1000)

    const killInterval = () =>
        clearInterval(interval)
}
```
