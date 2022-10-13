<!-- .slide: data-background="lime" -->
# What is Module Federation?


<!-- .slide: data-background="lime" -->
- New concept for sharing code between different bundles.

- First introduced in Webpack 5.

- Now also available as a framework agnostic library.


<!-- .slide: data-background="lime" -->
## Actually, what is a bundle?


<!-- .slide: data-background="lime" -->
- A bundle is a compiled JavaScript application.

- A collection of different JavaScript files,

- which are necessary to run the application,

- Eventually in one big blob,

- Or in smaller chunks on top which knows where to find what.


<!-- .slide: data-background="lime" -->
<img src="./resources/imgs/bundles--dist-directory.png" style="height: 100vh; margin: 0" />



<!-- .slide: data-background="lime" -->
## What does it solve?


<!-- .slide: data-background="lime" -->
- Think of 2 differnt JavaScript applications provides as a bundle.

- Both have a dependency on Patternslib.

- Both are loaded in the Browser.


<!-- .slide: data-background="lime" -->
```html
<script src="./bundle-1.js"></script>
<script src="./bundle-2.js"></script>
```


<!-- .slide: data-background="lime" -->
<img src="./resources/module-federation.svg" style="height: 100vh; margin: 0" />


<!-- .slide: data-background="lime" -->
- Shared dependencies are only loaded once.
- Bundles can depend on modules from another bundle.




<!-- .slide: data-background="Yellow" -->
## A bit of history


<!-- .slide: data-background="Yellow" -->
Zack Jackson, 2018, [webpack GH issue #8524](https://github.com/webpack/webpack/issues/8524) 


<!-- .slide: data-background="Yellow" -->
<img src="./resources/imgs/zack-jackson.jpg" style="height: 100vh; margin: 0" />


<!-- .slide: data-background="Yellow" -->
<img src="./resources/imgs/gh-issue-8524.png" style="height: 100vh; margin: 0" />


<!-- .slide: data-background="Yellow" -->
- Wanted to build a web application
- Based on many mini applications - "micro frontends"
- Each depending on React
- Didn't work.


<!-- .slide: data-background="Yellow" -->
- Zack implemented his idea
- [Webpack PR #10351](https://github.com/webpack/webpack/issues/10352)
- Early 2020.


<!-- .slide: data-background="Yellow" -->
<img src="./resources/imgs/gh-pr-10352.png" style="height: 100vh; margin: 0" />


<!-- .slide: data-background="Yellow" -->
- Multiple small applications works together as if they were one.
- Suited for Front- and Backend.
- Big teams work on many small apps.




<!-- .slide: data-background="Blue" -->
## Module Federation in Plone


<!-- .slide: data-background="Blue" -->
- [PLIP 3211 - Mockup Redone](https://github.com/plone/Products.CMFPlone/issues/3211) was already in progress.
- Problem of integrating Add-Ons.


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/plip-3211--addons-1.png" />


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/plip-3211--addons-2.png" />


<!-- .slide: data-background="Blue" -->
Then at Ploneconf 2020:


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/ploneconf-mf-2020.png" />


<!-- .slide: data-background="Blue" -->
A year later...


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/plone-mf-twitter-1.png" />


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/plone-mf-twitter-2.png" />


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/plone-mf-twitter-3.png" />


<!-- .slide: data-background="Blue" -->
And at Ploneconf 2021:


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/ploneconf-mf-2021.png" />


<!-- .slide: data-background="Blue" -->
But still not working.


<!-- .slide: data-background="Blue" -->
Manfred Steyer helped out


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/manfred-steyer-twitter.png" />


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/mf-minimalexample-commits.png" />


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/bssp1.jpg" />


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/bssp2.jpg" />


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/plone-mf-twitter-4.png" />


<!-- .slide: data-background="Blue" -->
<img src="./resources/imgs/patternslib-issue-1041.png" />




<!-- .slide: data-background="Cyan" -->
# A minimal example


<!-- .slide: data-background="Cyan" -->
https://github.com/thet/module-federation-minimaltest


<!-- .slide: data-background="Cyan" -->
<img src="./resources/imgs/minimalexample-github.png" />


<!-- .slide: data-background="Cyan" -->
... show code


<!-- .slide: data-background="Cyan" -->
## Result


<!-- .slide: data-background="Cyan" data-transition="none" -->
<img src="./resources/imgs/minimalexample1.png" />


<!-- .slide: data-background="Cyan" data-transition="none" -->
<img src="./resources/imgs/minimalexample2.png" />


<!-- .slide: data-background="Cyan" data-transition="none" -->
<img src="./resources/imgs/minimalexample3.png" />


<!-- .slide: data-background="Cyan" data-transition="none" -->
<img src="./resources/imgs/minimalexample4.png" />


<!-- .slide: data-background="Cyan" data-transition="none" -->
<img src="./resources/imgs/minimalexample5.png" />




<!-- .slide: data-background="Blue" -->
# Integration in Plone


<!-- .slide: data-background="Blue" -->
Base webpack configuration files:

[`@patternslib/dev`](https://github.com/patternslib/dev)


<!-- .slide: data-background="Blue" -->
Module Federation main - or host - bundle:

[`@plone/mockup`](https://github.com/plone/mockup/)


<!-- .slide: data-background="Blue" -->
- All bundles registered under common prefix.

- Host bundle initializes all bundles with that prefix.

- No bundle needs to know from each other.


<!-- .slide: data-background="Blue" -->
... Show code




<!-- .slide: data-background="DarkViolet" -->
When creating new Plone addons, use bobtemplates.plone >= 6.0b14/6.0b15:

https://github.com/plone/bobtemplates.plone


<!-- .slide: data-background="DarkViolet" -->
When creating only a Pattern, use pat-PATTERN_TEMPLATE:

https://github.com/Patternslib/pat-PATTERN_TEMPLATE




<!-- .slide: data-background="Purple" data-background-image="./resources/imgs/thats_all_folks.svg" -->
