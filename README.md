<h1> <a href="#" style="text-decoration:none">A close to Vanilla <br />Javascript Component Library </a></h1>

Jails is a project that aims simplicity by keeping as close as possible to vanilla Javascript development, and in the same time automates tasks that help us to improve our **produtivity**.

## The front end problematic actual state

It seems that we missed the simplicity from the time we were building interface applications with vanilla javascript. Many of our tools, language, and browsers has evolved through the years but some ideas might leading us to a place with a lot of unecessary complexity for **the vast majority of our use cases**.

Those ideas that comes in form of frameworks and complex libraries are making us believe that every large application needs complex solutions or a huge paradigm shift.

We are loosing the benefits of reusing libraries already built in Vanilla Javascript because there's no framework that has **interoperability** in mind, that's why you have the same library being rewritten in many forms.

Also, along with complexity the performance delivered in applications using frameworks are often not as good as it should. So, we are paying the technical debt by ignoring important learnings from the past like: Unobtrusive JavaScript, Separation of Concerns and goold Javascript Functional technics.

## The Motivation

Jails is very lightweight and it was designed to give you enough power to write dynamic components with the ability to integrate with any vanilla javascript libraries without leading you to a obscure and dark complex concepts. It's intend to help you to write javascript applications in an elegant fashion using some good concepts of programming that are framework agnostic like: 

- Event Delegation
- Event Driven Architecture 
- Observer and PubSub patterns for store and component communication

## Best Scenarios to Use
Jails is a library with **separation of concerns** in its core philosophy, so its not a isomorphic library, it doesn't intend to solve all the problems in the web application world. It's fully focus on client side development.
So you can use it on any Server Side Rendered Apps, or Static Sites Generated Apps like :

- Nodejs SSR and SSG apps using template systems ( Nunjucks, Pug, Ejs, Handlebars, Mustache, Liquidjs, etc )
- PHP projects ( Laravel, Ruby on Rails, Wordpress, Drupal, Joomla, etc )
- Static generated apps ( Hugo, Astro, Jekill, etc )

## Not a good scenario 
It's not intended to solve all the problems, it is focus only on web applications, not recomended to use on SPA's and it's not a hibrid solution for mobile applications but it's pretty suitable for PWA's and Mobile using Web View's and it can be pretty fast and a good alternative before engage into a native path.