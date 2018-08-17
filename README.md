Material-UI Data Visualization Tutorial
---------------

This tutorial introduces some fundamental concepts that are helpful
to understand if you want to
learn how to visualize data using Material-UI.

# Introduction

I have been working with Material-UI now
since the release of
[v1.0.0-beta.3](https://github.com/mui-org/material-ui/releases/tag/v1.0.0-beta.3) on July 29, 2017. Over that time period I have worked on different projects
that cover a range of topics. From that experience and knowledge, I have come
up with a tutorial that hits the highlights of ideas people need
to know when visualizing JSON data coming from an
[API endpoint](https://stackoverflow.com/questions/2122604/what-is-an-endpoint).

The demos in the
[Material-UI documentation](https://material-ui.com/)
are an excellent starting
point to better understand how Material-UI works in the context
of one React component.

But if you want a better understanding of a slightly more complicated
real world Material-UI application this will hopefully serve your needs.

## Create React App

First and foremost I have decided to start out with all of the
tutorial demos using
[Create-React-App](https://github.com/facebook/create-react-app).

The Material-UI doc is an excellent example of a real world application,
however, the reason for using CRA is because if you look at the
[Material-UI doc](https://material-ui.com/) you will note that
it uses
[Next.js](https://nextjs.org/) at the core for driving its routing.

Initially, I thought ok, I want to build a Material-UI drawer system
that uses **Create React App** (CRA) instead of Next.js. At the time, I was relatively new to using Material-UI and thought "oh this would be easy".  Turns out it was more tricky than I initially thought and it ended up taking me
days to really come up with a solution I was happy with.

So saving people time on just this one simple concept seemed like something
that would be valuable to have documented.  From there, I started working on
a more sophisticated application that used
[Menus](https://material-ui.com/demos/menus/) instead of [Drawers](https://material-ui.com/demos/drawers/) and that added more knowledge to understand and think about. Fast forward about a year, and I am finally getting around
to writing all of these concepts up along with polishing up some nice
demos that elucidate the concepts.

All of the demos that this tutorial will reference uses
CRA which means they all come out of the box the same way with the
same cadence of commands.

```sh
npm install
npm start
```

## Github Worlds

Github Worlds is a set of repositories located inside this tutorial that shows simple visualization techniques using Material-UI
**[cards](https://material-ui.com/demos/cards/)**.  The idea behind the set of demos is that data is retrieved from the
**[Github Graphql API](https://developer.github.com/v4/)** and stored in static JSON files which are then retrieved from some cloud server and displayed inside a data visualization of Github API endpoints.  Eventually, (in the future) this data might come live from the Graphql API but for now (in order to reduce complexity of the demo) we decided to use a simpler approach of static JSON files.

# The set of repositories discussed in this tutorial

All of the repositories in this tutorial use the
[MIT License](https://en.wikipedia.org/wiki/MIT_License) and are referenced with the **Github Topic** [material-ui-tutorial](https://github.com/search?q=topic%3Amaterial-ui-tutorial&type=Repositories).  They include in order of complexity from the most simple to slightly more sophisticated code:

## The List

* [mui-drawer](https://github.com/stormasm/mui-tutorial-demo/tree/master/mui-drawer)
* [mui-menu](https://github.com/stormasm/mui-tutorial-demo/tree/master/mui-menu)
* [ghw-autosuggest](https://github.com/stormasm/mui-tutorial-demo/tree/master/ghw-autosuggest)
* [ghw-drawer](https://github.com/stormasm/mui-tutorial-demo/tree/master/ghw-drawer)
* [ghw-menu](https://github.com/stormasm/mui-tutorial-demo/tree/master/ghw-menu)
* [mui-md](https://github.com/stormasm/mui-tutorial-demo/tree/master/mui-md)

### mui-drawer

There are two standard ways to navigate inside Material-UI; **[drawers](https://material-ui.com/demos/drawers/)** and **[menus](https://material-ui.com/demos/menus/)**.  The software for the [AppDrawer](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/AppDrawer.js) is located inside Material-UI **[docs](https://github.com/mui-org/material-ui/tree/master/docs#material-ui-docs)** and is not part of a released NPM repo (yet).  Therefore, I have broken out the drawer code into this demo to show how to use it standalone in the context of Create React App instead of Next.js which is how it is currently implemented.  The key minor change or refactor is to use
[React Router](https://github.com/ReactTraining/react-router) instead of Next.js for the routing.

### mui-menu

This is the exact same concept as above with the **mui-drawer** but instead of using drawers it uses Material-UI menus to navigate down to a specific React component.

### ghw-autosuggest

Github worlds (ghw) demo similar to the Material-UI demo
**[Autocomplete](https://material-ui.com/demos/autocomplete/)**
in the context of the Github worlds data.

### ghw-drawer

Github worlds (ghw) demo using Drawers as the driver for navigation.

### ghw-menu

Github Worlds (ghw) demo using Menus as the driver for navigation.

### mui-md

This demo shows how to integrate
[Markdown](https://www.markdownguide.org/getting-started) files into your Material-UI application.  Besides using
**[Typography](https://material-ui.com/style/typography/)**, Markdown is an excellent and simpler way to display your text without having to worry about the formatting issues associated with Typography.

**[MarkdownDocs](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/MarkdownDocs.js)** is used through out all of the Material-UI demos.  There is not an example of how to use it standalone and so I have come up with a nice simple demo that uses the MarkdownDocs code slightly modified.

**[MarkdownElement](https://github.com/mui-org/material-ui/tree/master/packages/material-ui-docs/src/MarkdownElement)** is the core software behind MarkdownDocs.  MarkdownElement is a part of the Material-UI distribution and lives inside the docs package.  Therefore this demo shows how to create a wrapper around MarkdownElement which is essentially the core mission of MarkdownDocs.

Besides the above two pieces of code another part of the demo shows how to use
**[React Markdown](https://github.com/rexxars/react-markdown)**.

All of the Markdown files that are displayed in this demo are loaded remotely from some server that gets defined in the demo code. It gives one the ability to have a static Markdown File Server for any Markdown files you want to display in your application.

# Next.js to Create-React-App

If you look at the Material-UI docs the main piece of Navigational software is the
[AppDrawer](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/AppDrawer.js)
which is derived from
[Drawer](https://material-ui.com/api/drawer/).

This section is about refactoring AppDrawer from Next.js to Create-React-App

This section will outline the details of how to transform the
[Material-UI Docs](https://material-ui.com/)
from Next.js to Create-React-App through a simple code
example.  

The example code for this section is in the github repository
[mui-drawer](https://github.com/stormasm/mui-tutorial-demo/tree/master/mui-drawer).  All code
references not referring to the
actual Material-UI
[docs code base](https://github.com/mui-org/material-ui/tree/master/docs#material-ui-docs)
will refer to the code inside **mui-drawer**.

## The AppDrawer Concept

Currently the Material-UI docs
[AppDrawer](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/AppDrawer.js)
are driven by
[Next-js Routing](https://nextjs.org/docs/#routing)
by using the Material-UI
[Link](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/Link.js) component.
In order to transform the
[Drawer](https://material-ui.com/demos/drawers/)
from Next-js to
[React-Router](https://reacttraining.com/react-router/core/guides/philosophy)
one must remove references to the Next-js Link inside the
[AppDrawerNavItem](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/AppDrawerNavItem.js)
and replace it with the React-Router
[Link](https://reacttraining.com/react-router/web/api/Link).

## The AppDrawer Details

If you take a look at the Material-UI docs and open the drawer
you will notice that all of the content inside the drawer is defined
by an an object called **pages** which is located inside the file
[withRoot](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/withRoot.js).

Inside this file are two other important functions.

* findActivePage
* getChildContext

These 3 pieces of code are ported over to their own file
in the sample code called
[Drawer](https://github.com/stormasm/mui-tutorial-demo/blob/master/mui-drawer/v1/src/containers/Drawer.js)

This code is the basis for the refactor.

## The AppDrawer Code

[mui-drawer](https://github.com/stormasm/mui-tutorial-demo/tree/master/mui-drawer)
is a demo that allows you to navigate inside
the drawer and show an example delineating a **Chapter**
in a book and a **Section** inside of the chapter.

Along with the **pages** object and the two functions
mentioned above this code is the other piece of logic
located inside the file
[Drawer](https://github.com/stormasm/mui-tutorial-demo/blob/master/mui-drawer/v1/src/containers/Drawer.js)
that completes the refactor.


```js
const ShowChapterSection = ({ match }) => (
  <div>
    <h3>Chapter: {match.params.ch}</h3>
    <h4>Section: {match.params.sec}</h4>
  </div>
);
```

## More Details

[See this Readme](https://github.com/stormasm/mui-tutorial-demo/blob/master/mui-drawer/code.md)
for more details on how to refactor the Material-UI code.

# Data Visualization Framework

I am in the process of developing a simple generic data visualization
framework in the context of a Material-UI tutorial with the main goal of
using this framework as a test bed for elucidating different aspects of
Material-UI.  So the tutorial and the framework will develop over time
in parallel.  As more interesting aspects of the framework get developed
the associated documentation teaching the Material-UI concepts of how it works will follow.

## The Overall Architecture of the framework

The concept is simple.  The framework supports views and JSON data.  

The views are any React component that can be accepted inside
[withStyles](https://material-ui.com/customization/css-in-js/#api).
The first example of this is a
[Grid List](https://material-ui.com/demos/grid-list/) with
[Cards](https://material-ui.com/demos/cards/) inside them.

The JSON data comes from any API call or endpoint that returns JSON data.  The API call can be GraphQL, REST, or static JSON data sources such as JSON files sitting on your local disk or in your Github repo.

## Github World Views

The tutorial repository for Ghw is called **ghw-menu** and is
[located here on Github](https://github.com/stormasm/mui-tutorial-demo/tree/master/ghw-menu).

Github World (Ghw) is a set of views coming from the [Github API](https://developer.github.com/v4/).
Using this data visualization framework one can develop new views of data for repositories, users, statistics and anything else that can be derived from this data possibly in concert with other data sets.

The data sets for Ghw are abstracted away from the underlying visualization so that the only thing needed to display the data is a JSON data file.  Eventually, we will provide a live view of the data coming from the Github API; but for now with simplicity being urgent we decided to only require JSON data sets.  The generation of the JSON data sets is described in another part of this document.  For now, we are providing a test set of JSON data files to better understand the structure of the data along with the program which interprets the data and a sample set of views.

Users are welcome to generate out their own custom views along with the data sets to their liking.

### One repo many views

In the current incarnation of the demo there are four views.

 * view1: vertical scrollable gridlist of cards
 * view2: horizontal single line scrollable gridlist of cards
 * view3: table view with [react-autosuggest](https://github.com/moroshko/react-autosuggest)
 * view4: vertical scrollable gridlist of cards with no avatars

### One view many repos

Each view in the system is accessible via the Views menu.  The repo dropdown
allows one to switch between different Github repositories while staying on the same view.  If you select a different repo the same view will be persistent.

### High level data flow outline

In all Create-React-App (CRA) applications things kickoff inside **index.js**.  From there you wire up the
[Redux](https://redux.js.org/introduction)
state through a Provider interface inside **Root**.  Next up is the **MenuAppBar** which houses the Icons and Menus along with the
[React-Router](https://reacttraining.com/react-router/core/guides/philosophy)
Route definitions.  Finally, when you select a view inside the menu Views.

**ShowTheLocation** will select the proper **DataViewWrapper** given the repo name and view name as
[props](https://reactjs.org/docs/components-and-props.html#props-are-read-only).

### DataViewWrapper

This component has two important variables defined inside it.

```js
const repoMap = {
  repo1: "material-ui.json",
  repo2: "graphql-js.json",
  repo3: "html5-node-diagram.json",
  repo4: "nodejs-sandboxed-fs.json",
  repo5: "ivy.json"
};
```

The **repoMap** allows one to define their own repositories of
data that they are interested in observing, showing to others,
or using for your open source web site.  Say you have an open
source project on Github, and you want to show the world all of the committers
on the project.  Or provided you don't have too many stars, all of the
developers who starred or forked your repo.  This is the type of view
that might be interesting to you but with your own repositories data
instead of these sample data sets.

```js
const template =
  "https://raw.githubusercontent.com/stormasm/ghdata/master/data1/";
```

The **template** is the location of where your JSON data files live.
You can put them anywhere you want, provided you define the template variable.

#### Fetching Data

Now that you have things defined, its time to go out and
[fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
the data.  For now we are fetching static JSON files from a specific
Github repo defined in the template above, but we could have just as easily fetched the data from the
[Github Api](https://developer.github.com/v4/).  
Or if you have other custom data views defined, your own GraphQL or
REST endpoint.

### DataView

DataView is a switch or set of if statements to grab the selected View from the View Menu in the AppBar.

The actual views themselves are styled any way you like them with
Material-UI's [styling solution](https://material-ui.com/customization/css-in-js/#material-ui-39-s-styling-solution).  

The **View** is the core of the application in that this is where you do your creative work.  Its your canvas so to speak, to create your data visualization. The rest of the framework is there for your use, you just have to be inventive
and come up with interesting views of your data.

The View takes in the prop **tileData** which is the data that was fetched from the API in the DataViewWrapper.  Then the tileData is mapped onto each component that you define in your View.

Any custom view that you define will take in tileData as a prop and then its up to you to build out your own styled component View.

### DataView Examples

#### AppBar

At the top of the hierarchy are ways to organize information or
websites.  All websites need to have an
[AppBar](https://material-ui.com/demos/app-bar/).  A nice example
of an AppBar in action is the
[Material-UI Home Page](https://material-ui.com/).
There you will
see the Icon button for drawer open and close.  In the repos
in this tutorial you
will see the same functionality.

#### Gridlists

The Gridlist is used to display a collection of Cards in both
a single horizontal line and with three cards per row.

#### Cards

The cards in this demo contain different data types about
each user that commits to a Github
repository including:
  * the user's name
  * the user's location
  * the user's username
  * a link to the avatar of the user

One can also grab data surrounding stars and forks as well.

#### React-Autosuggest

The Autosuggest is used to sort through many rows of a table and only display
particular users that are from a location that gets selected from the list
of user locations.  There may be more than one user displayed depending
upon how many users there are that reside in a particular location.

# Appendix

## Learning React

If you are coming to React for the first time and are in the learning process of understanding it:

**Be Patient !**...

Once you get React it makes total sense and is clear and easy to understand; but the road to get there can take some people awhile to grok. If you are fluent in more than one language; and you learned the second language as an adult you know how hard it is to get a concept.  Once you got it, you forget how hard it was to get there.  Computer programming is the same idea.  It takes years to truly be good at writing software; but once you are there it is just second nature.  React is not to this level of complexity... But it does take some people awhile.

The React model is truly the next evolutionary step in user interface design.  When you think about computer design and how one transistor can be scaled up to have
**[billions of transistors in one integrated circuit](https://en.wikipedia.org/wiki/Transistor_count)** and then
you think about Facebook and the thousands of components that exist inside
its total application you can begin to understand the power of React.

And that is also where Material-UI starts to shine.  The power of Material-UI and in general **CSS in JS** is not apparent at first look.  But as you start to develop large scale applications and then you realize that **WOW** I can just take this component that I used somewhere else; and drop it right down in my completely other unrelated application is when the light goes on.  Especially because all of the CSS comes along with it.  You no longer need to mess around with pulling CSS out of a much larger CSS file and then merge it into your new application's CSS file.

## Generating out Github Worlds JSON data files

For more details on how to generate out JSON data from the
**[Github GraphQL API](https://developer.github.com/v4/)**
check out the README for
**[Graphql Redis Github](https://github.com/stormasm/graphql-redis-github/blob/master/README.md)**.

## Links of Interest

 * [Material-UI v1 is out blog post](https://medium.com/material-ui/material-ui-v1-is-out-e73ce13463eb)

 * [A Journey Towards Better Style](https://oliviertassinari.github.io/a-journey-toward-better-style/#/0?_k=hwphr3)
and the **[github repo](https://github.com/oliviertassinari/a-journey-toward-better-style)**

* [All You Need To Know About CSS-in-JS](https://hackernoon.com/all-you-need-to-know-about-css-in-js-984a72d48ebc)

# About this document

This document is created using the awesome github repository
**[spec-md](https://github.com/leebyron/spec-md)**

This document is located inside
**[this github repository](https://github.com/stormasm/mui-tutorial/blob/master/ghw.md)**.

## Examples of spec-md docs...

The initial motivator for spec-md was
**[graphql](http://facebook.github.io/graphql/draft/)**

The actual
**[spec on spec-md](http://leebyron.com/spec-md/)**

## Living Document

If you are interested in participating in this project feel
free to
**[reach out to me](https://github.com/stormasm)**. I would welcome other developers
who are passionate
both about Material-UI and writing excellent
documentation. Making Material-UI more accessible to others
who are just getting started; and to those who
are experienced developers but want to have a well documented small
scale application that shows best practices for software development
in the Material-UI world.

If you have a cool idea about a new view married with the
[Github Github Graphql API](https://developer.github.com/v4/)
or just want to fix grammatical or spelling mistakes
in this tutorial you can find me on Gitter.

But for the most part, I hope you enjoy programming with Material-UI
as much as I do.
