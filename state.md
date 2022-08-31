# state 
`state : { get(), set() }`

> Reasonable way to manage data.

In many situations dealing with state is way better then updating ui using dom interfaces. In Jails, you can use the state helper to set and get the local state for your component and use it in html in order to react after state updates.

```html
<my-component>
    <p html-if="isVisible">{title}! now you see me</p>
</my-component>
```

*components/my-component.js*
```js
export default function mycomponent ({ main, state }) {

    main( _ => [
        show
    ])

    const show = () => {
        console.log('Current state', state.get())
        state.set( s => s.isVisible = true )
        //or
        state.set({ isVisible: true })
    }
}

export const model = {
    title:'Hello',
    isVisible :false
}
```

---

!> For more information about html directives available in the template system, jump into `Template System` section.