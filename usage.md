
# Usage

> Import library and components, register all your components for your page and then start application.

*main.js*

```js
import jails from 'jails-js'
import * as myComponent from './my-component'

jails.register('my-component', myComponent)
jails.start()
```

*html*

```html 
    <my-component>
        <h1>Hello World!</h1>
        <!-- More HTML Code -->
        <p>This is my simple component</p>
    </my-component>
```

*my-component.js*

```js
export default function myComponent ({ main, elm }) {
    
    main( _ => {
        console.log('Hello World!!!', elm)
    })
}
```

