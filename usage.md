
# Usage

### Markup
```html 
    <div data-component="my-component">
        ...
    </div>
```

### Javascript
*my-component.js*

```js
export default ({ main, elm }) => {
    
    main(() => [
        log
    ])

    const log = () => {
        console.log('Hello World!!!', elm)
    }
}
```

*main.js*

```js
import jails from 'jails-js'
import * as mycomponent from './my-component'

jails.register('my-component', mycomponent)
jails.start()
```