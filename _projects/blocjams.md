---
layout: post
title: BlocJams
date: 2015-08-11
feature-img: "img/blocjams_feature_img.png"
thumbnail-path: "img/blocjams_thumbnail.png"
short-description: At Bloc, I made a Spotify clone to learn the ropes of frontend development.
tags: [Git, HTML, CSS, JavaScript, jQuery]

---
## Summary
BlocJams was a crash course on the basics of frontend development, from language and tools to workflow and design. I was exposed to Git, text editors, HTML, CSS, JavaScript, jQuery all in the span of 3-4 weeks.

[View Site](http://kusera.github.io/bloc-jams/)

[View Code](https://github.com/kusera/bloc-jams)

## The Tools
The project began with an introduction to text editors and Git. While the syllabus creators at Bloc recommend Brackets, I was at home with Notepad++ and opted to author the project in that instead. I already had some experience with TortoiseSVN and TortoiseGit through my academic work, but at [Bloc](https://www.bloc.io) I resolved to become learn to use CLIs. The going was rough at first; I would often mess up commit messages, leading to liberal uses of `--amend`. The commits themselves were messy, with many small vaguely related changes, and sometimes I wrote the wrong message entirely. My Bloc mentor gave me a few rules to help keep everything nice and clean, rules I've been following since then:

1. Don't commit to the master/main branch
2. All branches should branch off of master
3. Merge branches to master via Pull Requests on GitHub, then pull to local master
4. Sync branches with 'git rebase'
5. Try to work on one branch at a time

Moving from GUIs to CLIs was rocky process, and I still feel more comfortable in a GUI environment, but I've since lost my anxiety over command lines. Using Git through a terminal has also taught me more about how Git actually works than Tortoise ever did.

## HTML and CSS
I toured modern HTML and CSS by creating a static mockup of the target product with a landing page, a collection page, and an album page. I had some prior experience with both languages so this segment was more of a refresher than a learning experience. Semantic tags like `<section>` and `<nav>` were new to me, and seemed like a reasonable feature at first, until I thought harder about what a `<section>` really was. I found resources like [HTML5 Doctor](http://html5doctor.com/lets-talk-about-semantics/) to guide my understanding, but eventually came to the conclusion that my time was better spent on fleshing out the project, rather than pondering the philosophical differences between `<section>` and `<article>` outside of news-based websites.

I learned more in creating BlocJam's CSS. Transform was a big surprise; they didn't exist in 2011, and that was when I picked up CSS. Being able to treat my block elements like objects in a game engine was pretty amazing, and transitions even moreso. Suddenly, many snappy animations websites use were demystified. I was under the impression web animation used to be done with scripts, so it was a pleasant surprise to discover I could tween the most common CSS properties with something as clear and simple as a transition.

Another "ah ha" moment was the discovery of media queries. I had absorbed terms like "responsive design" via osmosis, but had no idea what they referred to except that sometimes a website would adapt itself to my device's display size. I always thought the adaptation was achieved with multiple style sheets, and perhaps they once were, but now the problem has a more robust solution in media queries.

## From C++ to JavaScript
With the mockup done, I went through the process of adding functionality to the project like triggering CSS transitions, animating the seekbar, storing data inside nested objects, and DOM manipulation. Meanwhile, I was picking up JavaScript at a rapid pace.

I come from a C++/C# background, which allowed me to breeze through the absolute basics. I also had some experience with PHP, so while JavaScript's `var` wasn't a surprise, I found myself recoiling reflexively at weakly typed variables. Furthermore, I didn't understand the need for `===`, until I learned of JavaScript's automatic conversion between its primitives. Strict equality made a lot more sense once I viewed it in the context of `var`'s dynamic nature. Prototype inheritance was another case of culture shock where an unfamiliar, flexible system took the place of one that was rigorously structured.

I had encountered closures through C++11 (called lambdas) before. They didn't click immediately, and I never understood the benefits of closures until I delved into JavaScript. Being able to pass around functions as easily as objects made programming the UI much simpler than I was used to. I've attempted to create my own GUIs without the aid of libraries, and the resulting codebase, while usable, looked clunky and wasn't very extensible.

To actually give BlocJams full music player functioality, I refactored the entire project with jQuery, which cut down the verbosity, and I integrated the [Buzz](http://buzz.jaysalvat.com/) library so the site could actually play music. Integrating Buzz wasn't a big challenge, and gave me a taste of the vast array of plugins and third-party libraries available to frontend developers.

## Conclusion
BlocJams was a very instructive project. I covered more ground in 3 months than I have in an entire semester of some of my college courses, especially Introduction to Web Development. I'm glad I entered Bloc with a few years of programming under my belt; I might've been overwhelmed by the pace as a total novice. I wasn't satisfied with the final code base, however. BlocJams used `<script>` tags to insert all of its code into `index.html`. Functions were defined in the global scope. Even with the power of lambdas and jQuery, I would definitely describe some of the `.js` files as "spaghetti code". I brought up the concern with my mentor and he assured me that the next stage of Bloc, Projects, would teach me how to [solve that problem]({{ site.baseurl }}/projects/blocchat.html).
