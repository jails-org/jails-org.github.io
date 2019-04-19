
# Pub / Sub

> publish and subscribe functions dispatch global events, it's usefull when you want to broadcast a message to anyone who's subscribed to a message. *It's not a DOM event, it will not bubble up*.

Useful when you want to comunicate between components that hasn't a DOM parent/child relationship.
**subscribe** returns a **unsubscribe** function that can be called to remove that subscription.

---

### Modal Example

*components/some-component/index.js*

```js
export default ({ main, publish }) => {

    main(()=>[
        events
    ])

    const events = () => {
        on('click', '[data-open-modal]':openModal)
    }

    const openModal = () => {
        publish('open:modal', {msg: 'My message'})
    }
}
```

---

*components/modal/index.js*

```js
export default ({ main, elm, subscribe }) => {

    main(()=>[
        events
    ])

    const events = () => {
        subscribe('open:modal', open)
    }

    const open = ({ msg }) => {
        elm.classList.add('open')
        console.log('modal opened', msg)
    }

    //... more modal implementation
}
```

`Pub/Sub` is a global pattern, so in the example above, any component can open the modal by publishing `open:modal` and any component can subscribe to `open:modal` in order to be notified when modal is opened.

!> A publish is stored when called before the subscribe, the callback will be instantly called on subscribe in that case.
