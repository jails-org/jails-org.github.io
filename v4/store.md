# Store

> Don't be an accumulator, storage is like your bookcase, keep only the important stuff.

As we see in the previous section `State Management & Architecture` our component gets a `Msg` which is a single and local Store instance that provides us some interfaces that we can use to update the state by sending messages as actions. Jails create those intances automatically when you define and exports a `model` on your component module.

But those are just local stores instances that is being observed by just one component. If you want to create a Global store you need to create that instance manually, so you can export it and share with any component you want to listen to changes.

## Creating a Store instance

In the following example, we extract the store factory from Jails and create an instance to be exported to our application.

*stores/my-store.js*
```js
import { pandora, log } from 'jails.packages/pandora'

export default () => {

	const store = pandora({
		model,
		actions,
		middlewares: [ log('APP') ]
	})

	return store
}

export const model = {
    name :''
}

export const actions = {
    SAVE_NAME :( state, payload, store ) => {
        return {
            name : payload.value
        }  
    }
}

```

!> The store already comes with a middleware called **log**, is very usefull to debug store changes in the console. It will not log in production if you set **NODE_ENV** to `production` in your build process.

## Using the Store in Components

The code above will export a function that returns a store instance. You can't call it several times because you will loose the **Single Source of Truth** property and you will end up will several store instances.

So you have to create a single instance then use that on your components.
You can do that by sending your global store instance using `Dependency Injection`.

*home.js*

```js 
import jails  from 'jails-js'
import store  from 'stores/my-store'

// @Components
import * as mycomponent from '../../components/my-component'

const dependencies = {
	store  :store()
}

jails.register('my-component', mycomponent, dependencies)
//... more components here

jails.start()
```

*my-component.js*

```js
export default function mycomponent({ main, injection }) {

    const { store } = injection

    main( _ => [
        subscriptions,
        saveIntheStore
    ])

    const subscriptions = () => {
        store.subscribe( log )
    }

    const log = (state, {payload, action, haschanged}) => {
        console.log('HEY, I am a component using store!!!', payload, action, haschanged)
    }

    const saveIntheStore = () => {
        store.dispatch('SAVE_NAME', { value :'Clark Kent' })
    }

}
```

## API's

The store is just a `pub/sub` module, all the available methods you already seen in the previous section *State Management & Architecture* are available here too, all the **API's** are documented here : [https://github.com/jails-org/Packages/tree/master/pandora](https://github.com/jails-org/Packages/tree/master/pandora)

Check out the **Examples** section to see a use case in action.