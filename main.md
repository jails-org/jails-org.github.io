# main
``` main: () => void | Array<Function> ```
> In computer programming, an entry point is where the first instructions in a program are .... The main function is generally the first programmer-written function that runs when a program starts.

In Javascript, in order to execute a function you need to write the function before calling it. That can lead your code to be less readable because you will see implementation before understand the execution flow.

The `main` helper has a role to improve your code readability, like a table of contents of a book, and it was inpired by languages that uses it as a entry point, like `C/C++`, `Java`, `Go`, `Rust`.


```js
export default function MyComponent({ main }) {

    main( _ => {
         console.log(`Hi! I'm mounted!!`)
    })
}
```

---

!> The `main` function will get the same helpers of the exported function, you can use this feature to clean up the default exported function arguments.


```js
export default function MyComponent({ main }) {

    main( ({ on, off, trigger ... }) => {
        console.log(`Hi! I'm mounted!!`)
    })
}
```

!> You can also opt-in to return a set of functions that will be executed internally from Jails, so you can use this feature to keep your main cleaner.


```js
export default function MyComponent({ main }) {

    main( _ => [
        log
    ])

    const log = () => {
        console.log(`Hi! I'm mounted!!`)
    }
}
```