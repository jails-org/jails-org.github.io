# State Management & Architecture

> Reasonable way to manage data.

In order to manage a more complex data flow through your components you have to setup your component with some **interfaces** that will relate to each other making a unidirectional flow architecture.

Consider this markup as example for the following sections:

```html
<div data-component="my-component">
    <p v-if="isVisible">{{title}}! now you see me</p>
</div>
```

## Defining a Model

The Model represents all possible states your component will have. You just have to export a model variable.

*components/my-component.js*

```js
export default ({ main }) => {

    main(() => [

    ])
}

export const model = {
    title:'Hello',
    isVisible :false
}
```

## Defining Actions

Once you have a representation of all your states defined, then you need a way to change them. You do that, by using `Actions`.

```js
export default ({ main }) => {

    main(() => [

    ])
}

export const model = {
    title :'Hello',
    isVisible :false
}

export const actions = {
    
    TOGGLE_VISIBILITY : ( state, payload, {dispatch} ) => {
        return {
            isVisible : !state.isVisible
        }
    }
}
```

Your action is just a named function that will give you the current state, a payload, and the store instance as third parameter. We'll talk about that store instance in the next section.

## Changing State with Msg

You'll get the **Msg** helper function after defining a `model` for your component. 
It is just a instance of a Store that has some methods like : `set`, `getState`, `dispatch`, `subscribe`, etc. You will find more details about those methods in the **Store** section.

So, to change `isVisible` state using actions, you just have to `dispatch` that action.

```js
export default ({ main, Msg }) => {

    main(() => [
        changeVisibility
    ])

    const changeVisibility = () => {
        // Just passing an empty object to ilustrate that 
        // you can also send a payload optionally.
        Msg.dispatch('TOGGLE_VISIBILITY', {}) 
    }
}

export const model = {
    title :'Hello',
    isVisible :false
}

export const actions = {
    
    TOGGLE_VISIBILITY : ( state, payload, {dispatch} ) => {
        return {
            isVisible : !state.isVisible
        }
    }
}
```

!> The returned value will update only the desired state, it won't affect the others states like `title` in our example.

## Changing State without Actions

Sometimes the changes are really simple and you don't necessary need to be verbose using actions. You can just set a model and change the state using `Msg.set` interface.


```js
export default ({ main, Msg }) => {

    main(() => [
        changeVisibility
    ])

    const changeVisibility = () => {
        // This method doesn't expect any returned value
        Msg.set( state => {
            state.isVisible = !state.isVisible
        })
    }
}

export const model = {
    title :'Hello',
    isVisible :false
}
```

!> The `dispatch` and `set` methods triggers a state change in your component view.

## Defining a View

You will find many cases in your application where your markup gets a little messy with a lot of ternary expressions. Also, some variables from your model may not represent well what you're trying to do when you're in the markup context.

For those cases, you can filter and format your state before it goes to your markup view.

```js
export default ({ main, Msg }) => {

    main(() => [
        changeVisibility
    ])

    const changeVisibility = () => {
        // This method doesn't expect any returned value
        Msg.set( state => {
            state.isVisible = !state.isVisible
        })
    }
}

export const model = {
    title :'Hello',
    isVisible :false
}

export const view = (state) => {
    return {
        ...state,
        css :{
            visibility : state.isVisible? 'is-visible' :''
        }
    }
}
```

```html
<div data-component="my-component" v-class="css.visibility">
    <p v-if="isVisible">{{title}}! now you see me</p>
</div>
```

!> The returned value from view has a different behavior then the returned value from Actions. In this particularly case, you can override the entire state if want to. Remember to pass down the state in order to get access in the view.