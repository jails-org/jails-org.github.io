# Packages

> A Realm containing a curated list of great packages found on github plus some official packages developed for Jails.

The Jails Project was created with interoperability in mind and it has to be compatible with **ANY** javascript library. 

Therefore, there's no reason to develop solutions that is already there and don't need to be dependent on Jails library. We already have a huge javascript community that works on amazing projects.

## The Repository

There's a [Jails packages](https://github.com/jails-org/Packages) repository created with the purpose of to list all those amazing projects that are common on web development, so you don't need to remember them when you need to use them, plus the **Jails Official Packages** that has modules that extends Jails or just wrappers of other libraries.

These modules can be installed and imported on your application just like any other github modules:

*package.json*
```js
{
    ...
    "dependencies":{
        "jails.packages":"jails-org/packages"
    }
}
```