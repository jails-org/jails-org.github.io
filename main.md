# main
``` main: () => Array<Function> ```
> In computer programming, an entry point is where the first instructions in a program are .... The main function is generally the first programmer-written function that runs when a program starts.

The `main` helper is a function that will execute a set of functions in order. In Javascript, in order to execute a function you need to write the function before calling it. That can lead your code to be less readable because you will see implementation before understand the execution flow.

It is intend to improve your code readability, like a table of contents of a book, and it was inpired by languages that uses it as a entry point, like `C/C++`, `Java`, `Go`, `Rust`.


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

---

!> Every function in `main` list will get the same helpers of the exported function, you can use this feature to clean up the exported function arguments.


```js
export default function MyComponent({ main }) {

    main( _ => [
        log
    ])

    const log = ({ on, off, trigger ... }) => {
        console.log(`Hi! I'm mounted!!`)
    }
}
```