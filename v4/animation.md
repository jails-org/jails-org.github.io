# Introduction

> The icing on the cake...

You can use animations just like any other javascript project, by toggling css classes on `HTMLElement`, or just by using any javascript animation library.

But there's a special case when you need a little help from Jails. When you use `Reactor` for Template system. By using some directive such as `v-if` will append or remove nodes from the `DOM`, that means you can't add transitions when an element is appended or removed.

For those particular cases, there's an extra steps you need to do in order to control **entering** and **exiting** animations.

---

## Adding & Removing Elements

When you use `v-if` you are telling to the template system that in case of `false`, that element and all child nodes will be totally removed from DOM and discarted from your application. In case of `true` the opposite happens and that element with your children will be appended to the DOM again.

```html
<div v-if="isVisible" class="some-element">
    <p>My paragraph with text...</p>
</div>
```

## Adding Animations 

You just need to choose which `HTMLElement` you want to animate on appending/removing. 
In our case, we'll choose to animate the `p` element.

So you need to define 2 properties:
- `data-key` : Needs to be a unique name or id for that element.
- `data-animation` : Needs to be an animation name you want to give for that animation.

```html
<div v-if="isVisible" class="box">
    <p data-key="my-paragraph" data-animation="box-animation">My paragraph with text...</p>
</div>
```

Now, we just need to add animations through Css classes for those cases where the element leaves and when it enters:

```css
.box-animation-enter, 
.box-animation-leave-to{
    opacity: 0;
}
```

## Transition Classes

In this section we'll cover more precisely the transition classes, it's heavily inspired in `Vuejs` just like the templating system. So this section is just a copy & past from `Vuejs` documentation.

**There are 6 classes applied for enter/leave transitions.**

1. `-enter`: Starting state for enter. Added before element is inserted, removed one frame after element is inserted.

2. `-enter-active`: Active state for enter. Applied during the entire entering phase. Added before element is inserted, removed when transition/animation finishes. This class can be used to define the duration, delay and easing curve for the entering transition.

3. `-enter-to`: Ending state for enter. Added one frame after element is inserted (at the same time v-enter is removed), removed when transition/animation finishes.

4. `-leave`: Starting state for leave. Added immediately when a leaving transition is triggered, removed after one frame.

5. `-leave-active`: Active state for leave. Applied during the entire leaving phase. Added immediately when leave transition is triggered, removed when the transition/animation finishes. This class can be used to define the duration, delay and easing curve for the leaving transition.

6. `-leave-to`: Ending state for leave. Added one frame after a leaving transition is triggered (at the same time v-leave is removed), removed when the transition/animation finishes.

![Transition Example](https://vuejs.org/images/transition.png)

!> Those class names will be appended to the `data-animation` value you previously defined on your `HTMLElement`.



