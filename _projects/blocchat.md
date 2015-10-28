---
layout: post
title: BlocChat
date: 2015-09-03
feature-img: "img/sample_feature_img_3.png"
thumbnail-path: "img/blocchat_thumbnail.png"
short-description: A persistent chat application made with React/Flux, inspired by Slack.
tags: [Git, HTML, CSS, gulp, npm, firebase, JavaScript, React, Flux]

---
## Summary
BlocChat is a single-page chat application I made at [Bloc](https://www.bloc.io). It is the first web app I made independently, according to a list of user stories supplied by Bloc. BlocChat was written in 4 weeks, using [React](https://facebook.github.io/react/) and [Flux](https://facebook.github.io/flux/) as the framework. It was also my first time using [Gulp](http://gulpjs.com/) as a build system and [npm](https://www.npmjs.com/) for package management.

[View Site](http://kusera.github.io/bloc-chat/)

[View Code](https://github.com/kusera/bloc-chat)

## React
After I finished [BlocJams]({{ site.baseurl }}/projects/blocjams.html), I was given a choice of frameworks to learn for the Projects phase at Bloc. While Bloc's standard syllabus used [AngularJS](https://angularjs.org/), I found myself drawn to ReactJS after some brief research, comparing AngularJS with EmberJS and ReactJS. Part of it was the cleanliness of the syntax, particularly JSX. It was also "new", relatively, and Angular2 was on the horizon, so I felt compelled to future-proof my education.

## Gulp
Before I started BlocChat, I wanted to evolve my method of deployment. In BlocJams I used `<script>` tags to inject my code into `.html` files. While they worked fine, I knew there were better solutions out there. I was also interested in using live-reload to save on precious keystrokes. My mentor pointed me to [Yeoman](http://yeoman.io/) at the beginning to bootstrap my application, but after playing with generators I felt like leaving scaffolding to Yeoman would deprive me of a valuable experience. I decided to [learn](http://tylermcginnis.com/reactjs-tutorial-pt-2-building-react-applications-with-gulp-and-browserify/) how to use gulp on my own. I also looked into Grunt, but I liked Gulp's pipeline notation more than Grunt's nested configuration.

## Flux and closurss
I began by blocking out BlocChat using only HTML and CSS. Once I had the look and feel down, I converted the HTML into React components. With that done, I began studying how to implement Flux.

> _To digress for a bit..._

> I've created a UI system for a game during my C++ coursework in college. It was a stack of menus, each composed of labels and buttons. Every update frame, my `GUIManager` class would ask the menu at the top of the stack if any buttons were selected. Clicking a button raised a flag, an enum named after a function like `NEXT_LEVEL`, and this enum would be processed by `GUIManager`, which was the only class that was aware of, or could change the game state. It worked, and it respected encapsulation, but it was limited, because each menu could only ever raise one function at a time, and there was no way to pass information to GUIManager. I was never fully satisfied with the result.

So, Flux, to me, wasn't just an interesting new tool, but a solution to a problem I've been mulling over for some time. I was amazed by the simplicity of Flux, on a conceptual level It respected encapsulation, but was also robust enough to exchange any amount of data between the view and model. I had already split BlocChat into two main components, `RoomBox` and `MessageBox` while creating the prototype, so they naturally took on the role of controller-views. I also created a third component to wrap the two, called `ChatController` which became another controller-view. I divided the functionality of my app between the three, so that no single component was at risk of becoming a "god class".

On the model side, I started with two stores, `RoomStore` and `MessageStore`, one kept track of rooms, the other kept track of messages. As the application grew, I also added a `UserStore` to remember information about the user. A fourth, `MemberStore`, was created to remember the list of active users in a room.

I would say that I understood how closures worked by the time I started BlocChat, but it was using them in my application that made me see their power. Passing functions to components via props was a liberating experience, because I could give responsibilities to UI components without ever making them aware of a world outside their own module. The controller-views were smart, the leaf components were dumb, but there were no sacrifices that had to be made in terms of complexity or functionality on either the view or model side.

In truth, the most difficult part of working with Flux is the circular nature of the file editing. I might add a new feature to a component, create an action to express that feature, edit a store so they respond to that action, and finally return to the component to read in something new from the store. The workflow can be dizzying, and made worse when multiple components might be listening to a single store. In the case of BlocChat, I'm glad I was consistent in naming my files; I feel it went a long way to help me keep track of my modules' relationships.

## Firebase
Unlike many chat applications, BlocChat rooms are persistent; all messages that were ever typed in a room are stored in the cloud. Bloc suggested using [Firebase](https://www.firebase.com/) to persist data, and in this case I felt no reason to stray from the script. I have only a little experience with SQL, so interfacing with a fully featured cloud service was more time-efficient.

The first time I tried to communicate with Firebase, I ran into a problem where the Dispatcher would attempt to resolve two actions simultaneously, which is apparently forbidden. It was here that I really learned the difference between "synchronous" and "asynchronous". When I clicked a button, I naively sent a write action to the dispatcher (to add a room locally) and a write request to the server (to add a room on the server). Since I was listening to the server for changes to the rooms, and using actions to send these changes to the stores, the two resultant actions collided in the dispatcher. The strange thing was that my mentor did not experience this error, likely because he is based in Europe, while I was in NY. The lag acted like an unexpected `setTimeout()`.

Once I routed all Firebase-related actions through `ChatAPI`, my server-communication workhorse, the problem was solved.

## Modal
Being new to web development, I had no idea what modals were called but always thought they were really neat. I implemented my own for BlocChat for room creation and changing the username. At the same time, I tried using React's CSSTransitionGroups to animate the modals popping in an out. While it worked, the experience wasn't as smooth as I'd have liked, and it was extremely limited to boot. Nesting animations was a big headache and buggy to boot.

## Conclusion
Compared to BlocJams, BlocChat felt more "real". I wrote the app from scratch, and integrated Firebase independently. At the same time I was using a proper framework with React/Flux, and professional tools like gulp and npm. The result was a clean, well organized code base for a working chat client. I am proud of it, even though I didn't have time to implement more features I had in mind. Some day I might revisit BlocChat to extend it further.
