---
layout: post
title: Sentrii
date: 2015-09-22
feature-img: "img/sentrii_feature_img.png"
thumbnail-path: "img/sentrii_thumbnail.png"
short-description: A visual guide for "warding" in the multiplayer game Dota 2.
tags: [Git, HTML, CSS, gulp, npm, JavaScript, React, Redux, Pixi, Mocha, ES6]

---
## Summary
Sentrii is a quick, visual reference to "warding" in the game [Dota 2](http://blog.dota2.com/). Unlike [BlocChat]({{ site.baseurl }}/projects/blocchat.html) or [BlocJams]({{ site.baseurl }}/projects/blocjams.html), Sentrii is an original concept. In addition to designing and authoring the content myself, I experimented with new technologies including [Redux](http://rackt.org/redux/), an alternative to [Flux](https://facebook.github.io/flux/), the testing framework [Mocha](https://mochajs.org/), and [Pixi.js](http://www.pixijs.com/), a 2D WebGL renderer library.

[View Site](http://kusera.github.io/sentrii/)

[View Code](https://github.com/kusera/sentrii)

## Inspiration
I was proud of the progress I made with BlocChat and BlocJams, my first two projects at [Bloc](https://www.bloc.io), but I wasn't satisfied with the products themselves. In both cases, I was only mimicking existing applications and following a checklist. I chose to create Sentrii in order to add a new dimension to my education: Solving real problems using web applications.

## The Problem
Dota 2 is a popular multiplayer game with hundreds of thousands of unique players every day, and I have been playing Dota and similar games for many years. With Sentrii, I hoped to leverage my knowledge to create something useful: An up to date, visual quick-reference to warding, an important part of being a support player in Dota 2.

Ward guides do exist, but [some are out of date](http://www.team-dignitas.net/articles/blogs/dota/1092/dota-2-ultimate-guide-to-warding), [some lack any  context](https://www.reddit.com/r/DotA2/comments/3gwofx/updated_warding_map_on_current_minimap/), and [some are too cluttered](https://steamcommunity.com/sharedfiles/filedetails/?id=358789918). Not that these resources aren't valuable, but most of them are texts meant to be studied. It's difficult to refer to them in the middle of a game.

So, Sentrii: An interactive, lightweight warding resource players could use on the fly. As a personal twist, I added information that I feel is valuable for support players, but isn't closely associated with warding and tends to be hidden away elsewhere, in wikis or videos or posts on Reddit.

## Design
I started Sentrii by creating some wireframes. Throughout the process I used feedback from my mentor and a close friend, also a Dota player, to guide my designs.

### First wireframe
![Mockup 1](https://github.com/kusera/sentrii/blob/master/wireframes/mockup_1.png?raw=true)

This is the first wireframe I made. The image in the middle is the [map](http://dota2.gamepedia.com/Map) of Dota 2, the game field. To the left are filters that can be toggled on or off, each associated with a family of dots that represent warding locations. The box on the right displays additional information per ward location, triggered by a click from the user.

I aimed for information density, but both the map and the text would've been too small, squandering the massive screen real estate available to modern devices.

### Second wireframe
![Mockup 2](https://github.com/kusera/sentrii/blob/master/wireframes/mockup_2.png?raw=true)

The second design was a moderate improvement. Undepicted is the modal that would open up in response to map interaction, allowing me to maximize the size of the map as well as the amount of text or images I could deliver as additional details. The [third design](https://github.com/kusera/sentrii/blob/master/wireframes/mockup_3.png?raw=true) was a rearrangement of the second, an attempt to fix the lopsidedness of the filters around the map. The result made the division of the filters less clear, however, so it was discarded. The [fourth](https://github.com/kusera/sentrii/blob/master/wireframes/mockup_4.png?raw=true) design improved the overall contrast of the site, and added the feature of toggling an entire category of filters on or off.

### Fifth wireframe
![Mockup 5](https://github.com/kusera/sentrii/blob/master/wireframes/mockup_5.png?raw=true)

The fifth and final design fixed the visual balance issue without wasting screen real estate, and also added a footer.

## Redux and ES6
One of the problems I ran into with BlocChat were async requests. I was attempting to store user sessions on a server and retrieve them before loading the BlocChat. In between vanilla Flux and Firebase, there didn't seem to be a convenient way to achieve this rather basic functionality. Instead of halting development of BlocChat, however, I scrapped the feature and moved on. However, [Redux](https://github.com/rackt/redux) came up repeatedly in my discussions about promises and deferreds with my mentor. The name stuck, and even though Sentrii has no use for promises, I decided to expand my knowledge of Flux by building Sentrii in Redux. Additionally, as most Redux resources are written with ES6/ES7 syntax, I used the opportunity to pick up ES6 as well.

My experience with Redux was tumultous. Conceptually, it uses the same unidirectional flow as Flux but the syntax is much trickier, and core concepts less immediately obvious. I know that I have only touched a fraction of what Redux is capable of so I'm interested in exploring the library in future projects. On the bright side, in between my exposure to Flux and the reduced verbosity of Redux, Sentrii's codebase is much cleaner than that of BlocChat's.

Learning ES6 was a greater success. I am really grateful for the existence of `let` and `const`, as someone who cut his teeth on C++ and C#. I never ran into the common issues with `var`, but they were always in the back of my head. With block-level scoping, I don't have to worry about that anymore. Arrow functions are very convenient to write as well, and the sharing of `this` between arrow functions and their enclosing functions sidesteps another common JavaScript pain point. Classes might be syntatical sugar for prototypal inheritance, but the syntax is familiar and, once again, more compact than the ES5 equivalent. Destructuring, defaults, rest and spread all make my life easier.

## Unit tests
I knew, through osmosis, the importance of unit testing in development, but I had no firsthand experience, so I tried my hand at writing unit tests for Sentrii with Mocha, Chai and Sinon. The tests were successful, and I could see how testing might drive development, but with only a few unit tests I sensed that writing a full testing suite for Sentrii would take as long as writing Sentrii itself. I will attempt unit testing again in the future, once I'm finished with Bloc and its time constraints.

## PixiJS
With PixiJS, I actually felt right at home. I have worked in OpenGL, DirectX, Flash and Unity, so I was no stranger to either low level or high level graphics programming. Sentrii wasn't graphically intensive, but I could see myself authoring games in PixiJS. My 'MapNodes.js' file was particularly nostalgic. I created a base class called `MapNode`, extending `Pixi.Graphics`. `MapNode` was then extended into further classes like `WardNode` and `BoxNode`. I also took full advantage of rest/spread to cut down on redundant code.

```javaScript
// MapNode.js
class MapNode extends Graphics {
  constructor(id, x, y, onClick) {
    super();
    ...
  }
}

export class WardNode extends MapNode {
  constructor(color, ...base) {
    super(...base);
    this.draw(color);
  }
  ...
}

// Elsewhere
newNode = new WardNode(attributes.color, point.id, point.x, point.y, handleClick);
```
In my initial design of the `MapNode` class, I was planning to use overloaded constructors, something that turned out to be impossible in native Javascript because it's weakly typed. In hindsight, it wouldn't have worked anyway and inheritance was the right choice, but I'm glad to have confronted the issue anyway. I believe it gave me a deeper appreciation of JavaScript and C++ both.

## Conclusion
In truth, Sentrii did not progress as far in 3 weeks as I would have liked. I spent a lot of time learning about Redux, about ES6, and about tests. I also fiddled with using `npm` as a build tool over `gulp`, before Windows defeated me with its obstinate approach to paths. On top of it all, Sentrii as a site is not complete unless it actually conveys meaningful information, which meant a lot of time playing Dota 2 to extract the information I needed. There were more features planned for the time frame I set for Sentrii, features I cut completely. I suppose this is an unavoidable part of development, but I still feel a little disappointed.

But unlike BlocChat, which was mostly a one-and-done educational project, I want to continue working on Sentrii. Ultimately, I'm happy to have designed and written an application on my own; it was a valuable experience, disappointment and all.
