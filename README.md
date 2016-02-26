# React.js Conf: The Good Parts


I had the amazing opportunity to attend React.js conf in San Fransisco last week thanks to a generous diversity scholarship from Facebook! Two full days of talks from the creators, contributors and users of React.js, and 600+ React enthusiasts from around the world there to take it all in. It was a great chance to meet other React-ers and share ideas in a place where it is completely acceptable to take your laptop out at breakfast or the bar and talk shamelessly about code.

From what I heard, tickets this year were incredibly hard to get and if you didn't have time to watch the live stream, here's my summary of 'React.js Conf: The Good Parts' and a plethora of links for cool resources I heard about from the talks and talking to other people.

[Nick Schrock's Keynote](https://www.youtube.com/watch?v=MGuKhcnrqGA&list=PLb0IAmt7-GS0M8Q95RIc2lOM6nc77q1IY&index=1) really set the tone for the conference, highlighting how **React has grown from a JavaScript library into its own ecosystem that can fundamentally advance web development and React Native is completely changing the way mobile apps are being built, with cross-stack engineers replacing platform specific roles and teams**. He also pointed out some pretty impressive figures - like the fact that the Facebook Ads manager and Groups iOS and Android apps share 85-90% of their React Native code and were built with a single team! Many of the features on the Facebook app are also already in React Native, one being the Facebook Friend's day video which you might have seen a couple of weeks ago!

[Ben Alpert's talk](https://www.youtube.com/watch?v=-RJf2jYzs8A) on 'Making great React Apps' touched on several ideas of what still needed to be improved in React and React Native including animations, gestures, rendering fast lists and tools for improving developer experience across React and React Native - like what if you could remove the need for setting up webpack/babel to quickly prototype a new project with just one file e.g. create app.js and just call 'react run platform=ios'?

The announcement of Draft.js, a **rich text editing library for React** from Facebook, got everyone pretty excited! Making input text bold, cut, copy, paste, adding custom transformations like the 'mentions/check-ins' that can be added for statuses on Facebook - Draft.js makes this all infinitely easier for your React Apps. [Isaac Salier-Hellendang's talk](https://www.youtube.com/watch?v=feUYwoLhE_4) explained how the library takes the good parts of the 'contentEditable' browser feature (native cursor and selection behaviour, native input events & key events, all rich text features, automatic autogrowing of elements, accessibility and that it works in all browsers) and applies the principles of React to turn it into a controlled component - like a Text Input field with an onChange event handler and the input value saved to a state. I definitely recommend watching the full talk if you're interested in the implementation details.

**Data handling in React** was a recurring theme throughout the two days with multiple talks highlighting the many different options out there. [Lin Clark's talk](https://www.youtube.com/watch?v=WIqbzHdEPVM) illustrated with her quirky code-cartoons made for a fun and extremely clear introduction to Flux, Redux and Relay.

In short, Flux is out, Relay is a bit too complicated and Redux wins.

But seriously, Redux cuts some of the complexity of flux by using functional composition instead of callback registration, has a single store with immutable state, is super declarative, is great for testing and makes hot reloading and time travel debugging possible. Relay on the other hand requires a GraphQL server which is a beast in itself and takes a lot more set up, but has the additional benefits of being able to handle caching, query optimisation and network errors and the readability that comes from co-location of queries and views. Relay also allows deferred queries (e.g. retrieval of the title and text of an article and comments later) and reduction in the the size of queries - relay retrieves data and puts it in a local cache so some query data can just be retrieved from the cache. [Jared Forsyth's talk](https://www.youtube.com/watch?v=-jwQ3sGoiXg) introduced Re-frame and Om/next, both ClojureScript libraries. Re-frame is like Redux but uses subscriptions to define how to get data from state, which can be memoized so subscriptions are reused between components and for those of you familiar with Redux, there's no need to do `connect(state, props)` in the container. Om/next is a Relay like library but without the need for a GraphQL server.

**Optimisation and performance improvement** were also mentioned repeatedly. [Aditya Punjani's talk](https://www.youtube.com/watch?v=m2tvYGCdOzs) about optimising the FlipKart mobile website for 2G connections in India introduced two really interesting ideas: the App Shell architecture instead of traditional server-side rendering (breaking down app into loading state, with placeholders for data and loaded state, with the loading state being displayed in the first paint of the page) and service workers, a very cool browser API which can be used to intercepts all network requests so you can choose to either retrieve data from cache (for offline use) or from the network.

[Bhuwan Khattar](https://www.youtube.com/watch?v=SnAq9tbeRm4&list=PLb0IAmt7-GS0M8Q95RIc2lOM6nc77q1IY&index=23) suggested some methods for speeding up start up time. Branches in code - e.g. when a/b testing can lead to slow start up times as all the modules for each branch need to be downloaded leading to lots of unneccessary overhead. This is difficult to optimise because the branch chosen might be dependent on runtime data. One of the solutions he suggested was inline requires for lazy execution - i.e. only require things when they are necessary rather than requiring all the modules at the top of the file. Another solution used by Facebook is to use a wrapper instead of 'require' - use the wrapper to require dependencies that are not needed on initial render - these are downloaded as necessary with a loading indicator being shown in the meantime.

In [Tadeu Zagallo's talk](https://www.youtube.com/watch?v=0MlT74erp60&list=PLb0IAmt7-GS0M8Q95RIc2lOM6nc77q1IY&index=30) on 'Optimising React Native' he showed how to profile apps using the simulator in Xcode - bring up the developer menu inside the simulator (Cmd-Z) and click 'start profiling' and then view in chrome. This brings up a handy menu in Chrome so you can see which functions take the longest to run. He also mentioned two things to remember: always add component keys for lists - React's DOM diffing algorithm uses the keys to check which items need re-rendering so add keys to make sure all the list items are not re-rendered and try to always use the shouldComponentUpdate lifecycle method to prevent re-render unless necessary.

One of the most exciting things for me was hearing about the **new Navigation API in React-Native** from [Eric Vicenti](https://www.youtube.com/watch?v=09ddrCaLo10). After struggling with the Navigator component for months, the new declarative version sounds like a much better solution, borrowing heavily from Redux to remove the state from within the component and using actions for transitioning between views. The new changes should also support deep linking with URIS, a feature thats highly desirable in mobile apps.  I still haven't had a look at the new version properly but it's now available as 'NavigationExperimental' in the latest release of React Native.

[Leland Richardson's talk](https://www.youtube.com/watch?v=V5N0Ukb8LGg) about **testing React Native** was also super exciting! Not only has he created a library 'Enzyme' to help with traversing the DOM tree when shallow rendering React, he's only just gone and created a complete mock of the entire React Native API! Enzyme has shallow, mount and render methods as well as methods to find nodes of a specifc type in the tree. And he's also created some handy examples of how to use both libraries!

[Jamison Dance's talk](https://www.youtube.com/watch?v=txxKx_I39a8) has really made me want to try the **Elm language**! I'd only ever heard of Elm so it was completely new to me but in short, Elm is a functional programming language that transpiles to JavaScript and runs in the browser. It has a static type system (so no run time errors!) and there's no 'null'!. Elm only has stateless functions and only immutable data. Jamison showed how Elm applications have a similar tree architecture to React apps with parent components passing data down to child components which then respond to user interactions by sending data back to their parents which then update the top level app state and cause the App to re-render. Updating of state in React can be done in a number of ways including different libraries discussed earlier like Redux or Flux, but in Elm there's a built in system for updating state using Observables. The tradeoff is between constraints and guidelines - if you trust the language designers to have made good decisions for you, it eliminates the need to try and decide between different libraries for your application and you can focus on the problems specific to your application domain. Jamison suggested that learning Elm could help you become a better React Developer and I think I'm going to give it a go!

There were also some cool tips/ideas from the lightning talks:
* A way of [making React Native code more reusable between iOS and Android](https://www.youtube.com/watch?v=Zoerbz5Mu5U) -  create a wrapper for components that uses Platform.OS to check the operating system
* [Nuclide IDE support](https://www.google.co.uk/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwj-94i49pXLAhWIPRQKHZmZCjAQtwIIIzAB&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3Df1Sj48rJE3I&usg=AFQjCNFpSdDtTxCbr9AXczLRW435MG61pA) for react-native to make the developer experience just like the web. There's now a react-native-debugger, react-native-inspector and the ability to add breakpoints!
* React Native for web! A way to build truly platform agnostic code, enable universal rendering and it comes with built in web accesibility!

And then there were some of the wackier talks on [Virtual Reality](https://www.youtube.com/watch?v=ty2bFeOdGeI), [Open-GL effects](https://www.youtube.com/watch?v=Xnqy_zkBAew&list=PLb0IAmt7-GS0M8Q95RIc2lOM6nc77q1IY&index=18) and [making an arduino-raspberry-pi-React powered version of Jeopardy](https://www.youtube.com/watch?v=GnIrNYtmRDg)!!

Overall the conference was an amazing experience and my list of 'new things to learn' has now grown completely out of hand!

# Links:

## Libraries/APIs

### For React
* [Draft.js - Rich Text Editing with React](http://facebook.github.io/draft-js)
* [Email templating using React - Oy-Vey](https://www.npmjs.com/package/oy-vey)
* [Gatsbyjs static site generator using React + Markdown](https://github.com/gatsbyjs/gatsby)
* Open GL for React!
  * [gl-react](https://github.com/ProjectSeptemberInc/gl-react)
  * [gl-react-dom](https://github.com/ProjectSeptemberInc/gl-react-dom)
  * [gl-react-inspector](https://github.com/ProjectSeptemberInc/gl-react-inspector)
  * [Gl Sandbox](http://glslsandbox.com/)
* [Falcor - Data fetching library by Netflix](http://netflix.github.io/falcor/)
* [Cycle.js - data flow architecture based on observables](http://cycle.js.org/)
* [Enzyme - JavaScript Testing utility for React that mimicks jQuery's API for DOM traversal](https://github.com/airbnb/enzyme)
* [Guide for using Enzyme with Webpack](https://github.com/airbnb/enzyme/blob/master/docs/guides/webpack.md)

### For React Native
* [NavigationExperimental - new declarative Navigator API](https://github.com/facebook/react-native/tree/a91466f84a178c147e5913be0cea3086c44a4526/Libraries/NavigationExperimental)
* [Cordova plugins for React Native](https://github.com/axemclion/react-native-cordova-plugin)
* [Open GL for React Native - gl-react-native](https://github.com/ProjectSeptemberInc/gl-react-native)
* [React Native Web](https://github.com/necolas/react-native-web)
* [A complete mock of React Native](https://github.com/lelandrichardson/react-native-mock)
* [Guide for testing React Native with Enzyme](https://github.com/airbnb/enzyme/blob/master/docs/guides/react-native.md)
  * [Example React Native tests with Enzyme](https://github.com/lelandrichardson/enzyme-example-react-native)

### Random...
* [Service Workers to support offline experiences, push notifications and loads more](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
* [Push Notifications using Google Cloud Messaging](https://developers.google.com/web/fundamentals/getting-started/push-notifications/)
* [Chrome api for speech recognition](https://developers.google.com/web/updates/2013/01/Voice-Driven-Web-Apps-Introduction-to-the-Web-Speech-API?hl=en)
* [Webpack plugin to install modules from 'import' statements](https://github.com/ericclemmons/npm-install-webpack-plugin)
* [API Archive of Jeopardy Questions!!](http://jservice.io/)
* [Track.js - Monitor and report JS errors in web applications](https://trackjs.com/)
* [Raygun.io - Crash reporting](https://raygun.io/)

## Developer Tools
* [React Native plugin for Visual Studio Code](https://github.com/microsoft/vscode-react-native)
* [Deco IDE for React Native](http://www.reactnative.com/deco-a-react-native-ide-with-live-prop-manipulation-and-a-component-manager/)
* [Nuclide with React Native including react-native-debugger, ability to add breakpoints and react native inspector, flow support](https://github.com/zertosh/NuclideReactNativeSampleApp)
* [HockeyApp - distribute beta versions of apps without using the app store](http://hockeyapp.net/features/)

# Explanations/Tutorials
* [Code-Cartoons - Cartoon Explanations of Flux, Redux and Relay by the wonderful Lin Clark](https://code-cartoons.com/)
