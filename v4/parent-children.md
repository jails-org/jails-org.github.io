
# Parent & Children Updates

Components states are self contained and will not leak to other components. But in many cases you need to use a parent state in your child component, you can do that by using `update()` function helper.

!> Every parent component updates, using `render` calls or `msg` dispatches/sets, will call a `update()` function on its child components sending a Global State to be used optionally by a child component.

### Example

```html
<div data-component="A">
    I'm component A and my name is : {{name}}
    <div data-component="B">
        I'm component B and my name is : {{myname}}
        But my parent name is : {{name}}
    </div>
</div>
```

*Component A*

```js 
export default function A ({ main, msg }){

    main( _ => [
        start
    ])

    const start = () => {
        msg.set( state => state.name = 'Clark' )
    }
}

export const model = {
    name : ''
}

```

*Component B (Child)*

```js 
export default function B ({ main, msg, update }){
    
    const lastname = msg.getState().name //Kent
    
    main( _ => [

    ])

    update( props => {
        msg.set( state => state.name = `${props.name} ${lastname}`)
        // state.name = 'Clark Kent'
    })
}

export const model = {
    name : 'Kent'
}

```


!> Its recommended to use specific model names in favor of generic ones on cases that a parent component is designed to pass down its state for child components, in this way you can avoid naming collisions. You can always use `data-static` as well if you want to bypass any parent updates.