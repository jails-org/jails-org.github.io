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

## .use / .extend
These methods are for extend `Jails`.

### .use
Used for decorate Jails or override some of its behavior.
This method expects a function that returns another function which gets the Jails instance to be override/extended, so the developer don't need to care how he should import `Jails` in his plugin.

```js
jails.use( () => jails => {
    //Do something with jails here...
})
```

Ex. [Logger](https://github.com/jails-org/Packages/blob/master/logger/index.js)

### .extends
Used for extend components with new helpers.
This method expects a function that gets options returns another function which gets the Base instance of the components containing all the utility helpers, you just need to append to that instance your new helper.


```js
jails.use( options => Base => {
    Base.mynewhelper = () => { ... }
    return Base
    //Do something with jails here...
})
```

Ex. [Reactor](https://github.com/jails-org/Packages/blob/master/reactor/index.js)
