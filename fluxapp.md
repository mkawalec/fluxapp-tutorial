
# FluxApp howto

## Some semantics

We've built FluxApp to exploit isomorphism. But not 'weak' isomorphism
in the sense many other frameworks approach the subject.  Each component
you create not only has code that can be executed on the server
properly, it actually does execute on the server. When you open a
FluxApp powered website it renders on the server, sends the results to
your browser and then lets the client side bootstrap on the rendered
website.

That causes the website to appear before your eyes in the matter of
milliseconds, while keeping all the advantages of client side rendering.
Even better, text-only clients like search engines don't have to execute
the JS themselves, they get it automatically without using any hacks
like external rendering services.

All of that while using React.

### Caveat 1, supported environments

As of writing this, we only support Hapi on the server side. This
doesn't mean that other servers cannot be supported, to the contrary, it
is a trivial matter to add a different server. Don't see your server?
Look into `lib/platforms`, add your server and help the world :)

### Caveat 2, multiple requests on the server side

There may (and probably will) be many requests processed by the server
at any given moment. Internally we separate the stores, actions and
dispatchers for multiple requests by giving them separate contexts.
Unfortunately before Node introduces multiple execution contexts at the
same event loop, it will only be possible to use context-dependent
methods like `getStore` or `getAction` from inside `statics.load`.
Otherwise it would be impossible to separate execution contexts.

## The boilerplate

Before we start we need to write some glue code to make FluxApp aware of
its environment, after that we'll be good to go.

You need two packages

    npm install --save fluxapp iso-fetch

The first one is FluxApp, the second our isomorphic file fetcher. You
can use any other isomorphic fetcher but this one suits us the best.
You then need browserify/webpack to make sense of modules, but I leave
this part of the setup for you.

### Server side

We need to tell `iso-fetch` we're on the server side, so when
initializing hapijs you have to add 

    var api = require('iso-fetch');
    api.init({ hapi: { server: hapi }});

Where `hapi` is the instance of Hapi server you use. Having that taken
care of we have to write some code to bind the FluxApp renderer to the
server.


### Client side

### Shared code

## The data flow

Here show a nice svg, data flow after an action is invoked

### Creating an action

### Binding a store to an action

### Listening to changes inside a component

### Posting an action

### See it in action with the example app

### Rendering on the server side

Notice that when the component renders on the server side only one
render execution happens and so `componentDidMount` does not render.



####### My notes, hazardous

We have action creators that fetch the data through isofetch, stores and the components. 

On the server side, we use separate fluxapp instances for every request,
this way they don't come in each others way.

- talk about how the requests are handled on the SS
- show what's needed to bootstrap on the SS
- show what is needed on the CS to bootstrap
- give an example of the API and how it works through isofetch
- the bootstrap of isofetch on the client and SS

- give the model of data flow in fluxapp
- how it's different from Reflux

- show how the state changes in fluxapp
