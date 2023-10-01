<h1> <a href="#" style="text-decoration:none">An Elegant and Minimalistic <br />Javascript Application Library</a></h1>

Jails is a project that combines the power of vanilla Javascript development with the simplicity and convenience of task automation. Our goal is to enhance your productivity by automating tasks and keeping the development process as straightforward as possible.

## The front end problematic current state

The current state of front-end development is presenting some challenges. It appears that we have lost the simplicity that came with building interface applications using vanilla JavaScript. While our tools, languages, and browsers have evolved over time, some ideas have led us down a path of unnecessary complexity for the majority of our use cases.

Frameworks and complex libraries have convinced us that every large application requires intricate solutions or a major paradigm shift. Unfortunately, this has caused us to overlook the benefits of reusing libraries built in vanilla JavaScript. The lack of interoperability in frameworks is the reason why we often see the same libraries being rewritten in various forms.

Moreover, along with this complexity, the performance of applications using frameworks is often not as optimal as it should be. As a result, we are accumulating technical debt by neglecting important lessons from the past.

However, there is hope for improvement. By refocusing on simplicity and leveraging the wisdom gained from previous experiences, we can find ways to enhance both the productivity and performance of our front-end development.

## The Motivation

Jails is a lightweight framework that empowers you to build dynamic components effortlessly. Its primary purpose is to seamlessly integrate with any vanilla JavaScript libraries, all while keeping you away from the realm of obscure and convoluted concepts.

By using Jails, you can write elegant JavaScript applications that adhere to some fundamental programming principles. These principles, which are framework-agnostic, include:

- Event Delegation: Efficiently managing events by delegating them to a higher-level element.
- Event Driven Architecture: Designing applications that are built around events and their triggers.
- Observer and PubSub Patterns: Facilitating smooth communication between stores and components through observation and publication/subscription mechanisms.

With Jails, you can enjoy the benefits of these programming concepts while maintaining a clear and straightforward development process.

## Best Scenarios to Use

Jails is a library that embodies the core philosophy of separation of concerns. It is not an isomorphic library, meaning it doesn't aim to solve every problem in the web application world. Instead, it is fully focused on client-side development. You can seamlessly use Jails in various Server Side Rendered Apps or Static Sites Generated Apps, such as:

SSR and SSG apps that utilize template systems like: 
- Nunjucks, Pug, Ejs, Handlebars, Mustache, Liquidjs, and more.
PHP projects like: 
- Laravel, Ruby on Rails, WordPress, Drupal, Joomla, and others.
Static generated apps like:
- Hugo, Astro, Jekyll, and more.

While this solution may not address all problems, it is specifically designed for web applications. It's worth noting that it's not recommended for use in SPA's or as a hybrid solution for mobile applications. However, it performs exceptionally well with PWA's and Mobile using Web View's or as Web Components. Additionally, it offers impressive speed and serves as a viable alternative before considering a native approach.