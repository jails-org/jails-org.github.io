# Dependency Injection

> A dependency injection system is a feature that helps you to decouple your components from your project dependencies. 

The **Dependency Injection** system can be used to share singleton instances between components, and also useful for testing, so you can stub any dependency.

You can even make your components more generic by making them behave accordandly with dependencies they receive, like a validation component that can expect a set of functions for validations which can vary from one project to another.

*home.js*

```js
import jails from 'jails-js'
import validators from 'helpers/validators'
import * as formValidation from 'components/form-validation'

const dependencies = {
    validators // A map of validators to be used : required, email, number, etc.
}

jails.register('form-validation', formValidation, dependencies)
jails.start()
```

*components/formValidation.js*

```js 
export default function formValidation ({ main, dependencies }) {
    
    const { validators } = dependencies
    
    main( _ => [
        // ... Do UI validations using validators
    ])
}
```