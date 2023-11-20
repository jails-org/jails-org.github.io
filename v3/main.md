# Main

> In computer programming, an entry point is where the first instructions in a program are .... The main function is generally the first programmer-written function that runs when a program starts.

Every Jails components are a high level function that gets a set of helpers that you can use to abstract some tasks and to program your components logic. The `main` function is one of these helpers, it starts a set of functions in a sequence, and send to them all helpers from the higher level component function.

**The `main` function is used to setup your component definitions when it's mounted.**

```js
export default ({ main }) => {

    main(() => [
        log
    ])

    const log = () => {
        console.log(`Hi! I'm mounted!!`)
    }
}
```

---

### Composing Components

You can compose different behaviors/logic with another component to separate different concerns:

```js
import trackings from './tracking'

export default ({ main }) => {

    main(() => [
        trackings,
        log
    ])

    const log = () => {
        console.log(`Hi! I'm mounted!!`)
    }
}
```
