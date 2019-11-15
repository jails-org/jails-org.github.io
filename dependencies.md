# Dependency Injection

> A dependency injection system is a feature that helps you to decouple your components from your project dependencies. 

The **DI** system can be used to share singleton instances between components, and also useful for testing, so you can stub any dependency.

You can even make your components more abstract by making them behave accordandly with dependencies they receive, like a validation component that can expect a set of functions for validations which can vary from one project to another.

*home.js*

```js
import jails from 'jails-js'
import * as validation from 'components/validation'
import validators from 'helpers/validators'

const dependencies = {
    validators
}

jails.register('validation', validation, dependencies)
jails.start()
```

---

*components/validation.js*

```js 
export default function validation ({ main, injection }) {
    
    const {validators} = injection
    
    main( _ => [
        // ... Do UI validations using validators
    ])
}
```