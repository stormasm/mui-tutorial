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
up with a tutorial that hits the highlights of concepts people need
to know when visualizing JSON data coming from an
[API endpoint](https://stackoverflow.com/questions/2122604/what-is-an-endpoint).

The demos in the
[Material-UI documentation](https://material-ui.com/)
are an excellent starting
point to better understand how Material-UI works.
This tutorial further expands those concepts with
a slightly more complicated
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
demos that illustrate the concepts.

All of the demos that this tutorial will reference uses
CRA which means they all come out of the box the same way with the
same cadence of commands.

```sh
npm install
npm start
```

# Github Worlds

Github Worlds, from here on shortened to **ghw**, is a set of repositories located inside this tutorial that shows simple visualization techniques using Material-UI
**[cards](https://material-ui.com/demos/cards/)**.  The idea behind the set of demos is that data is retrieved from the
**[Github Graphql API](https://developer.github.com/v4/)** and stored in static JSON files which are then retrieved from some cloud server and displayed inside a data visualization of Github API endpoints.  Eventually, (in the future) this data might come live from the Graphql API but for now (in order to reduce complexity of the demo) we decided to use a simpler approach of static JSON files.

## The List

All of the repositories in this tutorial use the
[MIT License](https://en.wikipedia.org/wiki/MIT_License) and are referenced with the

**[Github Topic:  material-ui-tutorial](https://github.com/topics/material-ui-tutorial)**

They include in order of complexity from the most simple to slightly more sophisticated code:

### Drawers

* [mui-drawer](https://stormasm.github.io/mui-drawer/)
* [ghw-drawer](https://muitool.github.io/ghw-drawer/)

### Menus

* [mui-menu](https://stormasm.github.io/mui-menu/)
* [ghw-menu](https://muitool.github.io/ghw-menu/)

# The Repositories

## mui-drawer

This demo displays the same concept as
[mui-menu](https://stormasm.github.io/mui-menu/) except the navigation is a function of **drawers** instead of
[menus](https://material-ui.com/demos/menus/).

The Material-UI [docs](https://material-ui.com/)
give an example of using a Drawer to navigate
to different parts of the documentation.  The
[AppDrawer](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/AppDrawer.js)
code uses Next.js [Link](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/Link.js)
for its routing.  This demo shows how to use
[react-router](https://reacttraining.com/react-router/web/api/Link)
for its routing instead of [Next.js](https://github.com/zeit/next.js#with-link).

There are two principal navigation options in Material Design; **[drawers](https://material-ui.com/demos/drawers/)** and **[menus](https://material-ui.com/demos/menus/)**.  The software for the **AppDrawer** is located inside Material-UI **[docs](https://github.com/mui-org/material-ui/tree/master/docs#material-ui-docs)** and is not part of a released NPM repo (yet).  Therefore, I have broken out the drawer code into this demo to show how to use it standalone in the context of Create React App instead of Next.js which is how it is currently implemented.  The key minor change or refactor is to use
[React Router](https://github.com/ReactTraining/react-router) instead of Next.js for the routing.

If you look at the Material-UI docs the main piece of Navigational software is the **AppDrawer** which is derived from
[Drawer](https://material-ui.com/api/drawer/).

This section is about refactoring AppDrawer from Next.js to Create-React-App

This section will outline the details of how to transform the
[Material-UI Docs](https://material-ui.com/)
from Next.js to Create-React-App through a simple code
example.  

### The AppDrawer Details

If you take a look at the Material-UI docs and open the drawer
you will notice that all of the content inside the drawer is defined
by an an object called **pages** which is located inside the file
[withRoot](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/withRoot.js).

Inside this file are two other important functions.

* findActivePage
* getChildContext

These 3 pieces of code are ported over to their own file
in the sample code called
[Drawer](https://github.com/stormasm/mui-drawer/blob/master/v1/src/containers/Drawer.js)

This code is the basis for the refactor.

### The AppDrawer Code

This is a demo that allows you to navigate inside
the drawer and show an example delineating a **Chapter**
in a book and a **Section** inside of the chapter.

Along with the **pages** object and the two functions
mentioned above this code is the other piece of logic
located inside the file
[Drawer](https://github.com/stormasm/mui-drawer/blob/master/v1/src/containers/Drawer.js)
that completes the refactor.


```js
const ShowChapterSection = ({ match }) => (
  <div>
    <h3>Chapter: {match.params.ch}</h3>
    <h4>Section: {match.params.sec}</h4>
  </div>
);
```

### More Details

In order to transform the
[Drawer](https://material-ui.com/demos/drawers/)
from Next-js to
[React-Router](https://reacttraining.com/react-router/core/guides/philosophy)
one must remove references to the Next-js Link inside the
[AppDrawerNavItem](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/AppDrawerNavItem.js)
and replace it with the React-Router
[Link](https://reacttraining.com/react-router/web/api/Link).

For the details on how to refactor the code from Next.js
to Create React App [review code.md](https://github.com/stormasm/mui-drawer/blob/master/code.md)
for more details on how to refactor the Material-UI code.

## mui-menu

This demo displays a simple example of how to use Material-UI
[menus](https://material-ui.com/demos/menus/) in concert with
[react-router](https://github.com/ReactTraining/react-router)
and
[react-redux](https://github.com/reduxjs/react-redux).

This demo displays the same concept as
[mui-drawer](https://stormasm.github.io/mui-drawer/) except the navigation is a function of **menus** instead of
[drawers](https://material-ui.com/demos/drawers/).

### The concept

When you read a text book in school the author breaks all of the information into higher levels called chapters and then within those chapters are more fine grained knowledge called sections.  This demo simulates that concept by building a framework to enable electronic navigation of information broken down into chapters and sections.  You can navigate around using the chapter menu drop down in the upper left hand corner of the screen and then within those chapters individual sections which are the menu items.  Play around with the demo to see how it works.

The only thing that is displayed on the screen is your location.  But that is enough to show that the navigation is working.  It is up to the developer to expand this concept if they so choose by adding in more information to your E-book.

#### Precursor to Github Worlds

You will see when you get into
**[Github Worlds Menu](https://muitool.github.io/ghw-menu/)**
that the menu items are the views instead of the sections and the chapters are actually the Github
repository you wish to view.

### Adding Dynamic Routes

Inside this demo is a proof of concept for how to add dynamic routes
to your application.  In this demo, the core route which is a **chapter**
is the first part of the URL and the **section** is the second part of the URL.  The combination of these two items is what drives the react router to its final destination.  Having the ability to dynamically modify the routes by adding in chapters is accomplished via the **Admin** icon which is between the Section menu and the Github Icon.

#### Keeping things in Sync

The
[KeyContainer](https://github.com/stormasm/mui-menu/blob/master/v1/src/containers/KeyContainer.js) is responsible for handling
route changes by

* changing the redux state via the
[Picker](https://github.com/stormasm/mui-menu/blob/master/v1/src/components/Picker.js)
* and pushing the new route onto the [History API](https://github.com/ReactTraining/react-router/blob/master/packages/react-router/docs/api/history.md)

By doing this the new route URL will show up in the address bar.

### React Router Redux

* [react-router-redux](https://github.com/ReactTraining/react-router/blob/master/packages/react-router-redux/README.md)
* [legacy react-router-redux](https://github.com/reactjs/react-router-redux)

This project has been deprecated and currently there is not a good well
known solution to keep the History API and the Redux state in sync so
I have forked the above repo and placed it inside this demo
and
[ghw-menu](https://github.com/muitool/ghw-menu).

### Future work

Eventually we will persist the new routes or chapters to
[localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
and add in another button to clear out the localStorage and reset the redux state machine.

But for now each application refresh in the browser resets the redux state machine.

## ghw-drawer

Github Worlds drawer is a visualization toolkit that provides
**Views** into JSON data that comes from the
[Github GraphQL API](https://developer.github.com/v4/).
It is called Github Worlds **drawer** because there is also a
**[Github Worlds menu](https://muitool.github.io/ghw-menu/)** which displays the same data and views
but with the
**[Menu](https://material-ui.com/demos/menus/)**
being the primary navigation element instead of the
**[Drawer](https://material-ui.com/demos/drawers/)**

This demo is an extension of
[mui-drawer](https://stormasm.github.io/mui-drawer/) and it is assumed that you have already reviewed the concepts and
documentation associated with that repo.

### A Data Visualization Framework

We are in the process of developing a simple generic data visualization
framework in the context of a
**[Material-UI Tutorial](https://stormasm.github.io/mui-tutorial/)**
with the main goal of
using this framework as a test bed for elucidating different aspects of
Material-UI.  So the tutorial and the framework will develop over time
in parallel.  As more interesting aspects of the framework get developed,
the associated documentation teaching the Material-UI concepts will follow.

### The Overall Architecture of the Framework

The concept is simple.  The framework supports views and JSON data.  

The views are any React component that can be accepted inside
[withStyles](https://material-ui.com/customization/css-in-js/#api).
The first example of this is a
[Grid List](https://material-ui.com/demos/grid-list/) with
[Cards](https://material-ui.com/demos/cards/) inside them.

The JSON data comes from any API call or endpoint that returns JSON data.  The API call can be GraphQL, REST, or static JSON data sources such as JSON files sitting on your local disk, your cloud server or inside your Github repo.

### Github World Views

The tutorial repository for *ghw* is called **ghw-drawer** and is
[located here on Github](https://github.com/muitool/ghw-drawer)
or simply click on the Github icon in the upper right hand corner
of the
[AppBar](https://material-ui.com/demos/app-bar/).

Github Worlds (ghw) is a set of views coming from the [Github GraphQL API](https://developer.github.com/v4/).
Using this data visualization framework one can develop new views of data for repositories, users, statistics and anything else that can be derived from this data possibly in concert with other data sets.

The data sets for *ghw* are abstracted away from the underlying visualization so that the only thing needed to display the data is a JSON data file.  Eventually, we might provide a live view of the data coming from the Github GraphQL API; but for now the priority is to only require JSON data sets.  The generation of the JSON data sets is described in another section of the tutorial.  For now, we are providing a test set of JSON data files to better understand the structure of the data along with the program which interprets the data and a sample set of views.

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

### Data Structure Examples

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
a single horizontal line and with six cards per row.

#### Cards

The cards in this demo contain different data types about
each user that commits to a Github
repository including:
  * the user's name
  * the user's location
  * the user's username
  * a link to the avatar of the user

One can also grab data surrounding stars and forks as well.

## ghw-menu

Github Worlds menu is a visualization toolkit that provides
**Views** into JSON data that comes from the
[Github GraphQL API](https://developer.github.com/v4/).
It is called Github Worlds **menu** because there is also a
**[Github Worlds drawer](https://muitool.github.io/ghw-drawer/)** which displays the same data and views
but with the
**[Drawer](https://material-ui.com/demos/drawers/)**
being the primary navigation element instead of the
**[Menu](https://material-ui.com/demos/menus/)**

### The Order

This demo is an extension of
[mui-menu](https://stormasm.github.io/mui-menu/) and it is assumed that you have already reviewed the concepts and
documentation associated with that repo.

There is an order to the demos in this
**[tutorial series](https://github.com/topics/material-ui-tutorial)**
and this one is the last tutorial to review.  We highly recommend reviewing the other tutorials first so that you get all of the background information you need prior to reviewing this tutorial.

* [mui-drawer](https://stormasm.github.io/mui-drawer/)
* [ghw-drawer](https://muitool.github.io/ghw-drawer/)
* [mui-menu](https://stormasm.github.io/mui-menu/)
* [ghw-menu](https://muitool.github.io/ghw-menu/)

### The Card Views

There are four views present in the Github Worlds drawer and menu demo series. They include in order of View appearance.

* Cards displayed six across in an infinite vertical column
* Cards displayed in a Horizontal Line
* Cards displayed as a function of
[react-autosuggest](https://github.com/moroshko/react-autosuggest)
in concert with
[Material-UI Tables](https://material-ui.com/demos/tables/)
* Cards displayed with no avatars


### High level data flow outline

In all Create-React-App (CRA) applications things kickoff inside **index.js**.  From there you wire up the
[Redux](https://redux.js.org/introduction)
state through a Provider interface inside **Root**.  Next up is the **MenuAppBar** which houses the Icons and Menus along with the
[React-Router](https://reacttraining.com/react-router/core/guides/philosophy)
Route definitions.  Finally, when you select a view inside the menu Views.

**ShowTheLocation** will select the properties that get passed into the **DataViewWrapper** given the repo name and view name as
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
[Github GraphQL API](https://developer.github.com/v4/), or if you have other custom data views defined, your own GraphQL or REST endpoint.

### DataView

DataView is a switch or set of if statements to grab the selected View from the View Menu in the AppBar.

The actual views themselves are styled any way you like them with
Material-UI's [styling solution](https://material-ui.com/customization/css-in-js/#material-ui-39-s-styling-solution).  

The **View** is the core of the application in that this is where you do your creative work.  Its your canvas so to speak, to create your data visualization. The rest of the framework is there for your use, you just have to be inventive
and come up with interesting views of your data.

The View takes in the prop **tileData** which is the data that was fetched from the API in the DataViewWrapper.  Then the tileData is mapped onto each component that you define in your View.

Any custom view that you define will take in tileData as a prop and then its up to you to build out your own styled component View.

# Appendix

## Learning React

If you are coming to React for the first time and are in the learning process of understanding it:

**Be Patient !**...

Once you get React it makes total sense and is clear and easy to understand; but the road to get there can take some people a while to grok. If you are fluent in more than one language; and you learned the second language as an adult you know how hard it is to get a concept.  Once you got it, you forget how hard it was to get there.  Computer programming is the same idea.  It takes years to truly be good at writing software; but once you are there it is just second nature.  React is not to this level of complexity... But it does take some people a period of time.

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

## Markdown Processing in Material-UI

**[mui-md](https://github.com/stormasm/mui-md)**
is still in beta code but depicts using Markdown
in your applications.

This demo shows how to integrate
[Markdown](https://www.markdownguide.org/getting-started) files into your Material-UI application.  Besides using
**[Typography](https://material-ui.com/style/typography/)**, Markdown is an excellent and simpler way to display your text without having to worry about the formatting issues associated with Typography.

**[MarkdownDocs](https://github.com/mui-org/material-ui/blob/master/docs/src/modules/components/MarkdownDocs.js)** is used through out all of the Material-UI demos.  There is not an example of how to use it standalone and so I have come up with a nice simple demo that uses the MarkdownDocs code slightly modified.

**[MarkdownElement](https://github.com/mui-org/material-ui/tree/master/packages/material-ui-docs/src/MarkdownElement)** is the core software behind MarkdownDocs.  MarkdownElement is a part of the Material-UI distribution and lives inside the docs package.  Therefore this demo shows how to create a wrapper around MarkdownElement which is essentially the core mission of MarkdownDocs.

Besides the above two pieces of code another part of the demo shows how to use
**[React Markdown](https://github.com/rexxars/react-markdown)**.

All of the Markdown files that are displayed in this demo are loaded remotely from some server that gets defined in the demo code. It gives one the ability to have a static Markdown File Server for any Markdown files you want to display in your application.

## Links of Interest

 * [Material-UI v1 is out blog post](https://medium.com/material-ui/material-ui-v1-is-out-e73ce13463eb)

 * [A Journey Towards Better Style](https://oliviertassinari.github.io/a-journey-toward-better-style/#/0?_k=hwphr3)
and the **[github repo](https://github.com/oliviertassinari/a-journey-toward-better-style)**

* [All You Need To Know About CSS-in-JS](https://hackernoon.com/all-you-need-to-know-about-css-in-js-984a72d48ebc)

# About this document

This document is created using the awesome github repository
**[spec-md](https://github.com/leebyron/spec-md)**

This document is located inside
**[this github repository](https://github.com/stormasm/mui-tutorial-src)**.

## Editing this document and pull requests

Please read this section carefully and understand it prior
to issuing a pull request on the tutorial.

This document has several pieces which all come together to form
the tutorial.  If you want to understand how the tutorial gets built simply **[read the bash script.](https://github.com/stormasm/mui-tutorial-src/blob/master/scripts/buildme)**

So there are three main pieces to the tutorial and they are:

* [ghw-part1](https://github.com/stormasm/mui-tutorial-src/blob/master/ghw-part1.md)
* [ghw-part2](https://github.com/stormasm/mui-tutorial-src/blob/master/ghw-part2.md) **which gets built by the script**
* [ghw-part3](https://github.com/stormasm/mui-tutorial-src/blob/master/ghw-part3.md)

### ghw-part2 in more detail...

The file, **ghw-part2** gets built by the script and is a concatenation
of all of the *README.md* files in all of the tutorial demos in a particular order that flows and reads like a book or tutorial.  So it is important if you are editing any of these files that you keep that in mind.  **Do Not** edit the files in the repository
[mui-tutorial](https://github.com/stormasm/mui-tutorial), but rather edit the individual README.md files in the respective demos or

* ghw-part1
* ghw-part3

For more details on what you need to do to build this tutorial
[read this document](https://github.com/stormasm/mui-tutorial-src/blob/master/buildnotes.md)
as well.

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
