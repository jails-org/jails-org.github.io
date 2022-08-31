# onupdate 
``` ( fn:Function( props: Object ) ) => void ```
> A function callback that sends parent props to children components

This helper takes a callback that will be executed when parent component is re-rendered. Parent component will always update children components, you can use it to get parent props and update the children component.

---

```js
import jails from 'jails-js'
import * as mycomponent from 'components/my-component'

jails.register('my-component', mycomponent)
```

*components/my-component.js*

```js
export default function mycomponent ({ main, elm, unmount }) {

    main( _ => [
        
    ])

    onupdate((props) => {
        console.log('Getting parent props', props)
    })
}
```