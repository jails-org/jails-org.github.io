
# How does Jails Works?

Jails uses the Custom Element Browser api in order to define and encapsulate your component and its Html markup.
It will bind your javascript module to that custom element, your component module default function will get a set of functions tools as parameters that you can use to :

- Manage state 
- Update html
- Bind events 
...etc 

So Jails will do the hydratation on your html element but it will only contain the logic, the view will be already set in your html. In order to keep a html component dynamic, Jails compiles in runtime the html content of that component and will use it for further updates as you change the component internal state.

---

#### Development mindset 

The way to contruct web pages using Jails is to build your html independently from the library, using some Server side Rendering or using some Static Generation tool, then you just need to find where you app needs to be dynamic, like a form, or where there's a user interaction and place your Jails component and html directives on that section.

The thing is, your entire page does not need to be fully dynamic, there are many scenarios that you have only some parts of the page that actually needs to change or that will have some user interaction.

This way, or logic code is decoupled from html, it will be lightweight because it will not contain html definitions on it and will be more easy to understand and maintain.
