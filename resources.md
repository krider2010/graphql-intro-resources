## Resources

This is a collection of resources that might be useful...

This is the current [GitHub GraphQL Schema](https://developer.github.com/v4/public_schema/schema.public.graphql) - but be sure to check it's the latest.

### :hammer: Tools :wrench:

There are many tools available now for GraphQL, especially if you end up writing a GraphQL API. These tools are listed to help you make requests to GraphQL APIs as they have all been used by folk at GitHub and come recommended.

#### GraphiQL

This is a GUI for editing and testing GraphQL queries and mutations. The [app](https://electronjs.org/apps/graphiql) is an Electron wrapper around a JavaScript tool. Downloads are provided, along with command line instructions for some operating systems. The various panes for queries, responses, and documentation make this very simple to explore APIs with.

#### Insomnia

[Insomnia](https://insomnia.rest/) is a sweet client that can be used with REST as well as GraphQL and has tooling around templating and chaining to make it more rounded than GraphiQL. However it's less specialised in terms of the documentation support.

Once you have installed Insomnia, I have created a workspsace so that you can import the GraphQL endpoints setup with basic environment. You will need to customise this to add your own authentication token though.

[![Run in Insomnia}](https://insomnia.rest/images/run.svg)](https://insomnia.rest/run/?label=GitHub%20GraphQL&uri=https%3A%2F%2Fgithub.com%2Fkrider2010%2Fgraphql-intro-resources%2Fblob%2Fmaster%2FInsomnia_GitHub_GraphQL.json)

#### Altair Client

[Altair](https://altair.sirmuel.design/) is similar to GraphiQL in being a tool just for GraphQL. It has support for things like subscriptions and can be run in the browser via extensions as well as stand alone apps.

#### jq

[jq](https://stedolan.github.io/jq/) is like `sed` for JSON data. You can use it very much like those sorts of command line tools. It also has a lot of value just as a pretty printer which is what piping output through it will do by default.

#### fx

[fx](http://fx.wtf/) is more of an interactive JSON tool for the command line. Piping JSON through this tool allows you to explore the structure with mouse or keyboard and not just scroll a huge swathe of JSON. You can also use this tool just to pretty print output as well.

### :books: Reference Material :books:

Other things that may or may not have been mentioned in the Workshop that may be of interest!

* [GraphQL Specification](https://graphql.github.io/graphql-spec/)
* [Relay Cursor Connections Specification](https://facebook.github.io/relay/graphql/connections.htm)
https://facebook.github.io/relay/graphql/connections.htm
* The official [GitHub Octokit GraphQL](https://github.com/octokit/graphql.js) client, in JavaScript

