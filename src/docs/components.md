# Components

> Components are not Html Elements, Components are abstractions over them.

Basically, Components are functions that takes a set of utility helpers as arguments.
You can use those helpers to avoid manual and recurrent tasks and also use the best of them to create better abstractions for your application.

---

## Creating a Component

Every Jails components are scoped in to an HTML element, so first of all you need to tell where your component is gonna live.

```html
<div data-component="hello-world">
    ...
</div>
```

You can have as many components you want in the same markup:

```html
<div data-component="hello-world another-component other-component">
    ...
</div>
```

## Registering a Component

`Jails` will scan your html looking for `data-component` and then it will apply your registered component function on that Html Element. So before that scan, you need to register your component function.


`main.js`

```js
import jails from 'jails-js'

jails('hello-world', ( {init:main} ) => {

    main(() => [
        sayHi
    ])

    const sayHi = ( {elm} ) =>
        console.log( `Hello World! hello-world component is ready ! => ${elm}` )
})

jails.start() // Start scan and execute components main function.
```

## A Note about Code Design

The `Jails` register function takes 3 arguments, the first is the `name`, second is the component `Function`, and the third is `dependencies` which we'll cover it later.

So, to be more concise I suggest you to always keep your registration in your entry point main file, and your components in a separate one. In that way you can save some boilerplate and keep your code cleaner.

From now on, we will use that approach in the next examples:


`components/hello-world/index.js`

```js
export default ( {init:main} ) => {

    main(() => [
        sayHi
    ])

    const sayHi = () =>
        alert('HI!!')
}
```

`main.js`

```js
import jails from 'jails-js'

// @importing Components
import helloWorld from 'components/hello-world'

const dependencies = {
    injection :{}
}

// @Registering Components
jails('hello-world', helloWorld, dependencies)
//...

jails.start()
```


## Twitter Demo

It's not that complicated to setup a Jails app, but you can clone the [Twitter App](https://github.com/jails-org/Demos/tree/master/Twitter) in order to save some time and play with it a little.

The [Twitter App](https://github.com/jails-org/Demos/tree/master/Twitter) is also updated with Jails guidelines and best practices, you just need to clone it and you'll be ready to go!

---
