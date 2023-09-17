# About Jails Component
> The main and most important part of Jails Library, the **Components**. 

We're gonna understand how to build components using this library but in the same time we'll find which parts are gonna help us in tasks that would be more annoying in Vanilla Javascript development.

!> Typescript types are used in examples but they're not mandatory.
 
---

## Component Anatomy

Your component is a Javscript module that might contain 3 exported variables:

1. `export default Function` - **Required** - That is your component function.
2. `export const model <Object>` - **Optional** - Initial State for your component.
3. `export const view <Function>` - **Optional** - A middleware to filter current state before being passed to the html view.

<br />

*components/my-component.ts*

```ts
import { type Component, View, Model } from 'jails-js'

export default function myComponent( { main, elm, on, state, ... }: Component ) {
    // All javascript goes here...
}

export const model: Model = {
    
}

export const view: View = (state) => {
    return state
}
```

## Component Utility Helpers

Every Component function will get from Jails a set of javascript utilities properties, all of them are encapsulated in the scope of that current `HtmlElement`. Those utilities are not a set of functions like Lodash or Underscore, they are actually functions that help us on tasks we have in front end application. Like managing state, event handlers etc.

In the next Component sections we'll see each of these properties and what they do.


---

## The Benefits


### Encapsulation and Scalability 

The Jails role is to run the component function for each html element that match with the registered name using `jails.register` api, giving as parameters a set of utilities functions in order to design your component code and logic.

That means that even if you don't wanna use any of that utilities and just set plain vanilla js code you already will be benefit with the encapsulation running this function for each element in the page, so it scales up for **n** elements with the same logic in the page.

*main.js*
```ts 
import jails from 'jails-js'
import * as myComponent from 'components/my-component'

jails.register('my-component', myComponent)
```

*components/my-component.html*
```html
<my-component>
    <div class="my-component__content">
        <h1>Hello World</h1>
    </div>
</my-component>

<my-component>
    <div class="my-component__content">
        <h1>Hello World 2</h1>
    </div>
</my-component>

<my-component>
    <div class="my-component__content">
        <h1>Hello World 3</h1>
    </div>
</my-component>
```