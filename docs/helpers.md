# Helpers

Helpers are built-in scoped `functions` and `objects` passed to the High-Order function.

## .init

This is the most used helper and it should exist in every component. The role of this `function` is to execute a set of initial functions in the top of your high-order function, you can create all your functions below the `init()` definition and visualize quickly what does you component do when it starts just by looking at the top of your script.

**Child components are initialized before its parent components so you can be sure that a container component has its child components ready to be accessed/used.**

```js
//Using alias "main" for init, just to make it more ELMish
export default ( {init:main} ) => {

    main(() => [
        sayHello
    ])

    const sayHello = () =>
        console.log('Hello!!!')
}
```

**Important**: All the `functions` in the init/main list will get the same helpers from the high-order `function`.

## .elm

elm is a reference to the `HTMLElement` that contains the `data-component` definition.
Use this element as a context to search for child nodes using `elm.querySelector()` or
`elm.querySelectorAll`.

```js
export default ( {init:main, elm} ) => {

    main(() => [
        logElement
    ])

    const logElement = () => console.log( elm )
}
```

## .on

A function helper to add event listener that support `event delegation`.

```js
export default ( {init:main} ) => {

    main(() => [
        events
    ])

    const events = ( {on} ) => {
        on('click', componentClick)
        on('click', {'a':linkClick})
    }

    const componentClick = event =>
        console.log( 'Clicking in the component area', event.target )

    const linkClick = event =>
        console.log( 'Clicking in a child link element', event.target )
}
```

*Reminder* : **events** function gets the helpers from the high-order function through `init/main` call.
Use that when possible to make the high-order function definition cleaner.

**Important** : Always use `event delegation` so events can persist even if the child nodes are replaced to new ones.

## .off

A helper that removes a event listener.

```js
export default ( {init:main, off} ) => {

    main(() => [
        events
    ])

    const events = ( {on} ) => {
        on('click', componentClick)
    }

    const componentClick = event => {
        console.log( 'Clicking in the component area', event.target )
        off('click', componentClick)
        //Click will no longer log anymore
    }
}
```

**Important** : In the example above, the `off()` helper has to be defined in the high-order function. That's because `componentClick` is a event handler and it's not directly executed by `init/main` function.


## .emit

This handler emits **DOM Custom Events** an event to parent and siblings components. It is a way to communicate one component to another in a child -> parent direction.

The first parameter is any string you want, the second parameter optional data to pass on.

**Parent Component**

```js
export default ( {init:main} ) => {

    main(() => [
        events
    ])

    const events = ( {on} ) =>
        on('times-ellapsed', shout)

    const shout = (event, msg) =>
        alert( msg + '!!!' )
}
```

**Child Component**

```js
export default ( {init:main, emit} ) => {

    main(() => [
        events
    ])

    const events = ( {on} ) =>
        on('click', thisComponentClick)

    const thisComponentClick = event =>
        setTimeout( () => {
            emit('times-ellapsed','10 seconds elapsed since click')
        },10000)
}
```

Emit events are bubbled up just like any DOM Events.
They can be prevented just like any other event.

**Important** : You can only listen to custom events from child components or components that lives in the same markup.

## .trigger

This handler trigger a event or a custom event of a element. It also uses event delegation.

Triggering click in the component html element.
```js
trigger('click', {isparent:true})
```

Triggering click in a child html element.
```js
trigger('click', 'button', {ischildnode:true})
```

## .publish / .subscribe

publish and subscribe functions dispatch global events, it's usefull when you want to broadcast a message to any who is subscribed to that message. *It's not a DOM event, it will not bubble up*.

Useful when you have to relate components and they haven't a DOM parent/child relationship.
**subscribe** returns a **unsubscribe** function that can be called to remove that subscription.

`components/somecomponent/index.js`

```js
export default ( {init:main} ) => {

    main(()=>[
        events
    ])

    const events = () =>
        on('click', '[data-open-modal]':openModal)

    const openModal = () =>
        publish('open:modal', {msg: 'My message'})
}
```

`components/modal/index.js`

```js
export default ( {init:main, elm} ) => {

    main(()=>[
        events
    ])

    const events = () =>
        subscribe('open:modal', open)

    const open = ( {msg} ) => {
        elm.classList.add('open')
        console.log('modal opened', msg)
    }

    //... more modal implementation
}
```

`Pub/Sub` are global pattern, so in the example above, any component can open the modal by publishing `open:modal` and any component can subscribe to `open:modal` in order to be notified when modal is opened.

**Important** : A publish is stored when its called before the subscribe. The subscription callback will be instantly called on subscribe.

## .expose

This helper exposes a private `function`. All inner functions in the high-order function are private, so in order to access any of them outside you need to expose them.

`components/button/index.js`

```js
export default ( {init:main, elm} ) => {

    main(()=>[
        exposing
    ])

    // Making changeColor() public
    const exposing = ( {expose} ) =>
        expose( {changeColor} )

    const changeColor = ( color ) =>
        elm.style.backgroundColor = color
}
```

Now, we need a parent component in order to access that `changeColor` function. So lets learn how to do that by using the `get()` helper.

## .get

This helper is used when you need to get a child component through a parent component, and DOM and Pub/Sub are not sufficient.

You don't actually gets the child component, the helper gives you a reference to a child component and you can only execute the child component public functions.

*If you don't know how to make a private function public, please read the section `.expose` .*

The example below is a parent component of the component created in the previous example. So, in order to change the color in the child component lets get its reference and then call his public function.

`components/parentOfButtonCP/index.js`

```js
export default ( {init:main} ) => {

    const buttonComponents = get('button')

    main(() => [
        changeButtonsColors
    ])

    const changeChildColors = () =>
        buttonComponents('changeColor', '#336699')
}
```

You can pass a CssSelector as second parameter to get a specific component.

```js
export default ( {init:main} ) => {

    const buttonComponents = get('button', '.with-this-class')

    main(() => [
        changeButtonsColors
    ])

    const changeChildColors = () =>
        buttonComponents('changeColor', '#336699')
}
```

## .props

The props handler gets all the properties of the component `HTMLElement`, such as : `id`, `class`, `style`, `data` etc.

```html
<div data-component="user" id="my-user" data-options="{name:'Clark Kent', age :33}">
    <!-- ... -->
</div>
```

```js
export default ( {init:main, elm, props} ) => {

    const {options} = props('data') // Almost the same as elm.getAttribute('data-options')
    const id = props('id') // The same as elm.getAttribute('id') or elm.id

    main(() => [
        //...
    ])
}
```

The main difference between call `props()` instead of the DOM `.getAttribute()` is that getAttribute method will always return a `string` and `props` parses the value to the right type.

## .injection

Jails implements a simple system of dependency injection. It's possible to send all the dependencies for your components on registration, it will be accessible as a helper.

`home.js`

```js
import jails from 'jails-js'
import Store from '@SomePackage/Store'

import mycomponent from 'components/mycomponent'
import myOtherComponent from 'components/my-other-component'

const dependencies = {
    injection :{ store :new Store() }
}

jails('my-component', mycomponent, dependencies)
jails('my-other-component', myOtherComponent, dependencies)
// Other components

// Start jails scan
jails.start()

```

`my-component.js`

```js
export default ( {init:main, injection} ) => {

    const {store} = injection

    main(() => [
        registerStore
    ])

    const registerStore = () =>
        store.subscribe( update )

    const update = () => {
        //DO something when store updates...
    }
}
```
