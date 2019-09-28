
# Expose / Get

> Sometimes you need to execute a child function from parent...

All component's functions are private by default, in order to have access to a child function from a parent component, you need to `expose` that function in the child component, and then `get` it from his parent.

### Exposing a private function

*components/button/index.js*

```js
export default function button ({ main, elm })  {

    main( _ => [
        exposing
    ])

    // Making changeColor() public
    const exposing = ({ expose }) => {
        expose({ changeColor })
    }
        
    const changeColor = ( color ) => {
        elm.style.backgroundColor = color
    }        
}
```

Now, we need a parent component in order to access that `changeColor` function. So lets learn how to do that by using the `get()` helper.

### .get

Actually, You don't get the child component instance, the `get` helper gives you a reference to a child component and you can only execute the child component public functions.

The example below is a parent component of the component created in the previous example. So, in order to change the color in the child component lets get its reference and then call his public function.

*components/parentOfButtonCP/index.js*

```js
export default function parentOfButton ({ main }) {

    const buttonComponents = get('button')

    main( _ => [
        changeButtonsColors
    ])

    const changeChildColors = () => {
        buttonComponents('changeColor', '#336699')
    }
}
```

The default behavior is to find all components named as `button`, in the example above, and call the `changeColor` function in all components. 

---

If you need to specify which component you want to change, you can do so by passing a **CssSelector** as second parameter to get a specific component:

```js
export default function parentComponent({ main }) {

    const buttonComponents = get('button', '.with-this-class')

    main( _ => [
        changeButtonsColors
    ])

    const changeChildColors = () => {
        buttonComponents('changeColor', '#336699')
    }
}
```