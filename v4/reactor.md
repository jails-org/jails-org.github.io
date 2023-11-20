
# Render ( Reactor )

> An Interface to update DOM with a new state, using the fantastic  [SodaJs](https://github.com/AlloyTeam/sodajs) Template System.

You can either choose to change DOM directly or use Template System in Jails. To use the template system and update the view with a new state you have to extract `render` function helper and call it passing a **plain javascript object**.

!> Reactor uses [Morphdom](https://github.com/patrick-steele-idem/morphdom) in order to make **diffing** and optimize dom updates, if you choose to use template system, remember that if you do any dom changes manually, using `elm.classList.add` for instance, the next reactor update will discard that change. You can use `data-static` in order to bypass reactor dom changes to a specific node and its descendents.

### Usage

```html
<div data-component="my-component">
    <h1>Hi {{name}}</h1>
    <ul>
        <li>My Enemies</li>
        <li v-repeat="enemy in enemies">
            {{ enemy }}
        </li>
    </ul>
</div>
```

```js
export default function mycomponent ({ main, render }) {

    main( _ => [
        update
    ])

    const update = () => {
        render({
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

### API

#### plain

```js
const data = { name : 'Clark Kent' }
```

```html 
<div>{{name}}</div>
```

➜ [plain example](http://alloyteam.github.io/sodajs/pg/rd.html?type=simple)


#### safe propery chain output
```js
const data = {
    name: 'v',
    info: {
        version: '2.0'
    }
}
```

```html
<p>{{info.version}}</p>
<!-- result => "2.0" -->

<p>{{info.foo.foo1}}</p>
<!-- // result => ""  without errors -->

<p>{{info['name']}}</p>
<!-- // result => "2.0" -->
```

#### expression

```html
<p>{{1 + 2}}</p>
<!--  result => 2 -->

<p>{{true ? 'v' : 'foo'}}</p>
<!-- result => "v" -->

<p>{{1 < 3 && 'v'}}</p>
<!-- result => "v" -->
```

➜ [expression example](http://alloyteam.github.io/sodajs/pg/rd.html?type=expression)

#### complex expression

```js
const data = {
    list: [
        {list: [{'title': '<>aa</h1>'}, {'title': 'bb'}], name: 0, show: 1},
        {list: [{'title': 0 }, {'title': 'bb'}], name: 'b'}
    ]
}
```

```html 
    <h1>{{list[list[0].show === 1 ? list[0].name : 1].list[0].title}}</h1>
```

### Directives

### if

``` js
const data = { name : 'Clark Kent', show: true }
```

```html
<div v-if="show">Hello, {{name}}</div>
<div v-if="!show">I\'m hidden!</div>
<!-- // result => <div>Hello, v</div> -->
```

➜ [if example](http://alloyteam.github.io/sodajs/pg/rd.html?type=if)


### repeat

> v-repeat="item in array"

> v-repeat="item in object"

> v-repeat="item in array by index"

> v-repeat="item in object by key"

> v-repeat="(index, value) in array"

> v-repeat="(key, value) in object"

default index or key is $index

``` js
const data = {
    list: [
        {name: "Hello" ,show: true},
        {name: "sodajs" ,show: true},
        {name: "AlloyTeam"}
    ]
};
```

```html 
<ul>
    <li v-repeat="item in list" v-if="item.show">
        {{item.name}}
        {{$index}}
    </li>
</ul>
```

➜ [repeat example](http://alloyteam.github.io/sodajs/pg/rd.html?type=repeat)

---

### html

output origin html as innerHTML

```js
const data = { html : '<span style="color:red;">test v-html</span>' }
```

```html
<div v-html="html"></div>
```

➜ [html example](http://alloyteam.github.io/sodajs/pg/rd.html?type=html)

### replace
replace this node with html

```js
const data = { html : '<span style="color:red;">test v-html</span>' }
```

```html
<div v-replace="html"></div>
```

➜ [replace example](http://alloyteam.github.io/sodajs/pg/rd.html?type=replace)

div will be replaced with given html

### Others

#### v-class
> v-class="currItem === 'list1' ? 'active' : ''"

#### v-src
> v-src="hello{{index}}.png"

#### v-style
> v-style="style"

data example:

```js
const data = { style : { width : '100px', height : '100px' } };
```

#### v-*
> v-rx="{{rx}}%"

> v-checked="{{false}}"

if the value is false or "", the attribute will be removed