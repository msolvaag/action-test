# orchard-suite

This repository contains common Javascript modules which can be reused among Orchard javascript based implementations. It is built with [pnpm](https://pnpm.js.org/) and [changesets](https://github.com/atlassian/changesets).

## Packages

### General Guidelines

- Ensure that each package has its own README file which clearly explains how it can be used. This should likely include example code that illustrates how any exported classes, functions, etc. can be utilized.
- Add the package to the list of existing packages below, with a tl;dr about its purpose (and link it properly, please).

### Existing Packages

- [`@theorchard/suite`](./packages/suite) includes all you need to start building orchard suite apps.
- [`@theorchard/suite-components`](./packages/suite-components) common React components used in Orchard suite apps.
- [`@theorchard/suite-icons`](./packages/suite-icons) common icons and graphical assets used in Orchard suite apps.
- [`@theorchard/suite-identity`](./packages/suite-identity) utils and react hooks to manage Orchard user identities.

## FAQ

### Why do we need this?

There are non-trivial pieces of code that we use throughout our javascript apps/services at The Orchard which benefit from standardization. If you have non-trivial code that needs to be re-used across frontend or backend javascript implementations, this may be a good place for you to add such code.

### Isn't this a monorepo? Isn't that bad? I've heard that's bad.

There is a school of thought that says, yes, this is in fact a bad idea. However, many organizations such as [Facebook](https://www.youtube.com/watch?v=X0VH78ye4yY), [Google](https://www.youtube.com/watch?v=W71BTkUbdqE), and [Twitter](https://www.youtube.com/watch?v=bjh4DHuOf4E) have found value in this approach.

Now, it's pretty easy to put together a list of organizations and projects that do a thing a certain way and argue that the thing is great because of that. On its own, that's not a super compelling argument, so here are some Orchard-specific reasons why this is desirable:

- *If you need a new package, you don't need a new repository.*
- *If you need a new package, you don't need a new pipeline.*
- *If you need a new package, you don't need to repeat patterns for typescript, linting rules, unit test frameworks.*

### When is a good time to create a new package?

Keep in mind that a new package added to this repository can require ongoing maintenance: when you make changes you will have to increment build numbers, deploy new versions, and inform clients that there are new versions of the package available. Therefore, it's useful to consider how frequently your proposed package will be changed, before committing to adding it to this repository. 
For example, if you were to add an `@orchard/features` package to this repository containing all active feature flag enum values, this would need a version bump, a new deployment, and client updates every time feature flags were added/removed. That sounds like a lot of work, right? As a general rule, it's useful to add something to this repository *once you are sure that the initial version will be fairly static*. For example, the patterns used by [`@orchard/ows-data-source`](/packages/ows-data-source) were very well understood and iterated upon for quite some time before that package was upstreamed as a dependency. If we had added this package at the start, we would have had quite the headache each time the interface changed! So it's good to keep in mind that adding code here creates a bit of an internal API SLA between the author and the clients who will utilize the dependency.
