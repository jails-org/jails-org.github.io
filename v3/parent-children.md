
# Parent & Children Updates

Components states are self contained and will not leak to other components. But in many cases you need to use a parent state in your child component, you can do that by using `parent` property inside a state.

!> Every parent component updates, using `Reactor` calls, will force a re-render on its child components sending a Global State to be used optionally by a child component named as `parent`.

### Example

```html 

<div data-component="A">
    I'm component A and my name is : {{name}}
    <div data-component="B">
        I'm component B and my name is : {{name}}
        But my parent name is : {{parent.name}}
    </div>
</div>
```

!> Its recommended to use specific property names in favor of generic ones on cases that a parent component is designed to pass down its state for child components, in this way you can avoid some naming collisions. You can always use `data-static` as well in order to bypass any parent updates.