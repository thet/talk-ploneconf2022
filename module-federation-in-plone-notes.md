# Module Federation in Plone

If you follow the JavaScript world it's not unlikely that you have heard about something called module federation.

Module federation is a concept developed by Zack Jackson for Webpack which allows to import JavaScript modules from different builds.

With this technology, different bundles can share the same code without loading it multiple times. Still, all the bundles carry all of their dependencies and would be able to run on their own. But the webpack runtime with module federation support would make sure that the same code is not loaded and interpreted twice.


Why would that be important?

1) When used in a web environment the download size is kept down. If bundles share the same dependencies - which they often do, think of jQuery, React or even Mockup and Patternslib - you do not have to download the same resource / the same piece of code from different bundles multiple times.

2) The state is kept. We often store data on a module level scope - e.g. the value of a counter as an easy example. If you would use multiple versions of the same module each of them would have their own module-level counter value.
This can especially be a problem with jQuery. For example, one jQuery instance loads a specific plugin. If later another jQuery instance is loaded, it would overwrite the first one and effectively delete the plugin.

For this to work, webpack needs to split up the bundle in smaller chunks which can be loaded individually. Which is a good idea anyways - e.g. to enable dynamically importing and loading individual modules when needed.

Also webpack needs to add a runtime on top of the build which knows it's dependencies and is responsible to load them or reuse them if they were already loaded.


Now this opens up a lot of possibilities


Zack's idea dates back to late 2018 where he described a feature request in webpack GitHub issue #8524 [Micro Frontend architecture - many builds as one](https://github.com/webpack/webpack/issues/8524). He wanted to build a web application which consists of many micro frontend applications based on react. But when going from one micro frontend to another react would reload the page to load the next entry point. There is a webpack feature called externals which could be used to realize this idea, but this is also a bit of a hack without the possibility of fine grained control.

Zack then implemented his idea wich led to the webpack pull request #10351 [Merge Proposal: Module federation and code sharing between bundles. Many builds act as one](https://github.com/webpack/webpack/issues/10352) early 2020.

So, one of the first use cases was to architecture a web app consisting of many micro frontends which would act together as if they were a big monolith but still have all the flexibility of individual apps.

This does not only work in a web environment but is also perfectly suited for backend micro services.

A software architect's dream coming true, where many teams in a huge company would be able to work on their own delimited, small services while those services would also be able to work together and share and reuse code between each other.

When I came across this idea that rang a bell. In Plone 5 we had to configure named RequireJS stub modules for bundles to not include those in the final build. That feature is actually similar to webpack externals, but this does not scale well. Also no one understood RequireJS and the resource registry. We ended up with a very complex build system which had the purpose to manage our JavaScript dependencies and optimize our builds. And it was not even very flexible or scalable. But this was what we could offer at the time and when we created this at the Zidanca sprint in Slovenia in 2014, that was top-notch technology, bringing us leaps in front of other CMS or web frameworks which had often just no answer at all on how to manage an unknown set of dependencies added by system integrators at any time.

At Syslab we also had the requirement of providing JavaScript functionality on a modular level so that designers could add new features by just downloading different bundles from a web page and integrating it. We could not really fulfill this requirement other than always providing customized builds for each project.

When I first heard about module federation in 2020 I was immediately reminded on our situation in Plone and at Syslab. I made an vague and unproven hint at my Ploneconf talk in 2020 that this could solve our problems with JavaScript bundles in Plone 6. For the Plone conference 2021 I made a first proof of concept showing that different bundles would load the same resource only once. And after some preparation the module federation configuration helpers were merged into Patternslib at this year's Buschenschanksprint in May.

Plone 6 now uses module federation as a way to share dependencies between different bundles!


Let's take a look how we do that

The way we use it in Patternslib, Mockup and Plone goes with just little extra effort - or none at all if you use create your JavaScript with bobtemplates.plone or the pat-PATTERN_TEMPLATE generator. We simply expose all of the package's direct dependencies for sharing.

If different versions of the same dependency are requested, the highest compatible version is used or multiple versions are loaded.




Initial MF proposal:
Zack Zackson's GitHub Account:
Zack Jackson's Twitter Account: https://twitter.com/ScriptedAlchemy/


