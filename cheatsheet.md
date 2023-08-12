
# Template System

> An Interface to update DOM with a new state using html directives.

You can either choose to change DOM directly or use Template System in Jails. To use the template system and update the view with a new state you have to call `state.set` function helper passing a **plain javascript object** as a new state. 

!> For more information about internal state, jump to `state` section inside **Components**.


### Usage

```js
export default function myComponent ({ main, state }) {

    main( _ => [
        showInfo
    ])

    const showInfo = () => {
        state.set({
            name :'Clark Kent',
            enemies:[
                'Lex Luthor', 
                'Darkseid',
                'General Zod',
                'Brainiac'
            ]
        })
    }
}
```

```html
<my-component>
    <h1>Hi ${name}</h1>
    <ul>
        <li>My Enemies</li>
        <li html-for="enemy in enemies">
            ${enemy}
        </li>
    </ul>
</my-component>
```

### Changing default Delimeters

Jails sets internally the delimiters with a open and close braces `{` `}` only to keep as more simple as possible, but there are some situations where that can cause ambiguity if something on your html has the same open and close braces for other purpose rather for templating, in that case the template system will raise a syntax error. For those cases, the most simple way to fix that is to change default delimiters:

```js
jails.templateConfig({
    tags :['@{', '}']
})
```

Now you can use `@{ variable }` to display variable data and fix the template error for those cases.


### Cheatsheet

#### plain

```js
state.set({ name : 'Clark Kent' })
```

```html 
<div>${name}</div>
```

#### Safe propery chain output
```js
state.set({
    name: 'Clark Kent',
    info: {
        version: '2.0'
    }
})
```

```html
<p>${ info.version }</p>
<!-- result => "2.0" -->

<p>${ info.foo.foo1 }</p>
<!-- // result => ""  without errors -->

<p>${ info['name'] }</p>
<!-- // result => "Clark Kent" -->
```

#### expression

```html
<p>${ 1 + 2 }</p>
<!--  result => 2 -->

<p>${ true ? 'v' : 'foo' }</p>
<!-- result => "v" -->

<p>${ 1 < 3 && 'v' }</p>
<!-- result => "v" -->
```

#### complex expression

```js
state.set({
    list: [
        {list: [{'title': '<>aa</h1>'}, {'title': 'bb'}], name: 0, show: 1},
        {list: [{'title': 0 }, {'title': 'bb'}], name: 'b'}
    ]
})
```

## Directives

### html-if

``` js
state.set({ name : 'Clark Kent', show: true })
```

```html
<div html-if="show">Hello, {name}</div>
<div html-if="!show">I\'m hidden!</div>
<!-- // result => <div>Hello, Clark Kent</div> -->
```

### html-for
- `html-for` for arrays and objects

Iterable variables `$index` and `$key` is automatically generated.

> html-for="item in array"

> html-for="item in object"


``` js
state.set({
    list: [
        {name: "Hello", show: true},
        {name: "Clark", show: true},
        {name: "Kent"}
    ]
});
```

```html 
<ul>
    <li html-for="item in list">
        <span html-if="item.show">
            ${ item.name } 
            ${ $index }
        </span>
    </li>
</ul>
```

### html-inner
It's a innerHTML directive, that's an alternative way to display variable value, **and it's not escaped**.
```js
<p>My name is <strong html-inner="name">Some default value</strong></p>
```

`html-inner` directive will translate the code above to this:

```html
<p>My name is <strong>${name}</strong></p>
```

### html-model
In this directive you can send to your component a initialState that will override some attribute of your `model`.
**IMPORTANT: This directive has to be used on your component `HTMLElement`.**

```html 
<my-component html-model="{ counter: 5 }">
    <p>The counter initial value is: ${counter}</p>
    <!-- Or -->
    <p>The counter initial value is: <span html-inner="counter"></span></p>
</my-component>
```

---

## Attributes

#### html-*
You can prepend `html-` for all html attributes, the template system will strip them off. Very usefull for attributes that you need to be quiet on page load, like `src` until js is ready, you don't want to make any requests when before javascript parsing.

#### html-class
It will add to the existing className list if its already set
> html-class="currItem === 'list1' ? 'active' : ''"

#### html-src
> html-src="imageUrl"


## Boolean HTML Attributes
`selected` | `checked` | `readonly` | `disabled` | `autoplay`

They will evaluate an js expression or a variable and set the attribute if the expression is true, and remove attribute otherwise.

> html-checked="10 > 2"

```html
<input type="radio" html-checked="10 > 2" />
<!--  <input type="radio" checked /> -->

<input type="radio" html-checked="false" />
<!--  <input type="radio" /> -->

```