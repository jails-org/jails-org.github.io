# Events

> Simple Dom events with Event Delegation

Events are a powerful tool to sending messages from children to parent nodes, it's a widely adopted pattern and very familiar to javascript developers. Jails extends this feature with some sugar.

### .on
Like any other helper, this is binded to the current component, so event will be registered in the component custom element. It uses a very powerful technic called `event delegation`. This makes possible to listen to child nodes even if they are replaced with new nodes and simplify the way you bind events in child elements.

```js
export default function myComponent ({ main }) {

    main( _ => [
        events
    ])

    const events = ({ on }) => {
        on('click', componentClick)
        on('click', 'a', linkClick)
    }

    const componentClick = (event) => {
        console.log( 'Clicking in the component area', event.target )
    }

    const linkClick = (event) => {
        console.log( 'Clicking in a child link element', event.target )
    }
}
```

### .off

A helper that removes a event listener.

```js
export default function myComponent ({ main, off }) {

    main(() => [
        events
    ])

    const events = ({ on }) => {
        on('click', componentClick)
    }

    const componentClick = (event) => {
        console.log( 'Clicking in the component area', event.target )
        off('click', componentClick)
        //Click will no longer log anymore
    }
}
```

### .emit

This handler emits **DOM Custom Events** an event to parent and siblings components. It is a way to communicate one component to another in a child -> parent direction.

The first parameter is any string you want, the second parameter optional data to pass on.

**Parent Component**

```js
export default function parentComponent ({ main }) {

    main( _ => [
        events
    ])

    const events = ({ on }) => {
        on('time-ellapsed', shout)
    }

    const shout = (event, msg) => {
        alert( msg + '!!!' )
    }
}
```

**Child Component**

```js
export default function childComponent ({ main, emit }){

    main( _ => [
        events
    ])

    const events = ({ on }) => {
        on('click', thisComponentClick)
    }

    const thisComponentClick = (event) => {
        setTimeout(() => {
            emit('time-ellapsed','10 seconds elapsed since click')
        },10000)
    }
}
```

Emit events are bubbled up just like any DOM Events.
They can be prevented just like any other event.

!> You can only listen to custom events from child components or components that lives in the same markup.

### .trigger

This handler trigger a event or a custom event of a element. It also uses event delegation.

Triggering click in the component html element.
```js
trigger('click', {someparam:true})
```

Triggering click in a child html element.
```js
trigger('click', 'button', {anotherparam:true})
```
