# JEEP.COM FRONT PAGE PROJECT

I built this website replication from scratch as part of a coding challenge for a Software Developer postion with a startup in North Austin. You can see this project deployed on [Github Pages](https://multishifties.github.io/jeepfrontpage/) 

## Table of contents

* [technical specifications](#specs)

* [original website baseline](#baseline)

* [build process and differences](#project)

* [copy website performance](#tests)

* [if I had to do it over](#thoughts)

* [if I had to launch it into production](#production)

## Specs

The challenge is pretty straightforward. Recreate an exact copy of the current jeep.com front page. The only constraints specified by the client were that I must incorporate Twitter bootstrap in the build (no specific version. 3 and 4 are both acceptable). This application, just like the original page, must also be FULLY mobile responsive.

A preliminary examination of the jeep.com website indicates that they're using Webpack, React, jQuery, Google Analytics, and possibly an adobe CMS. I'll attempt to stick to the technologies in use and limit the use of any technologies, frameworks, or libraries that are not in use on the real website.

I'll be using Bootstrap version 4 (was in beta, stable version released as I was working on this project! AWW YEAH!!). However, bootstrap V4 no longer ships with Glyphicons! So I'll be including the font-awesome css for icon styling.

## Baseline

As of 1/11/2018 @ 5:30pm CST on a 2016 MacBook Pro 2.7 GHz Intel Core i5 running OSX 10.11.3, opened in Google Chrome version 63, over a Google Fiber internet setup operating at 52.7 Mbps down and 37.3 Mbps up; jeep.com's front page currently rates in at the following scores using Google Chrome's lighthouse auditing tool:

![alt tag](./imagesForReadme/lighthouse_scores.png)

45/100 on Progressive Web Application. Points of note include : 

* No firstMeaningfulPaint event in trace when throttled down to simulare 3g network speeds.

* Does not register a service worker, responds with 200 OK even when offline, no configured splash screen, and Address bar not matching brand colors.

(In all fairness, most all of these can be resolved with a manifest.json & service worker. But it's fair to point out that Google has been spearheading the whole push towards Progressive Web Applications, and not everyone is onboard with it yet. So it's the exception rather than the rule if a web application scores very well in this category. I'm honestly more concerned with fixing the 3G network speed issue than I am with the service workers and manifest)

0/100 on Performance

* All errors are related to the total size of the web page. At 132 network requests and 3.5MB of data, this website loads slower than most. DOMContent varies between 1.58 - 2.05 seconds, Load between 3.40-4.05 seconds. But network requests continue until Finish which varies between 10.27 and 11.88 seconds.

![alt tag](./imagesForReadme/network_metrics.png)

86/100 on Accessibility

* A few images are missing 'alt' attributes.

* A few ids are being used more than once on the page.

* While technically not listed under this section, the original website uses javascript to asynchronously load in assets and images after the document has loaded (usually a good thing to ensure faster initial page load). However, the original page does not provide a fallback notice or content (missing `<noscript>` tag) if JavaScript is Disabled. The same page still renders with javascript disabled, albiet with a lot of missing images and broken functionality. In my copy I've added a simple fallback notice requesting that the user enable javascript in their browser.

69/100 on Best Practices 

* Uses `document.write()`.

* Includes jQuery 1.11.2, which is outdated and may have security vulnerabilities.

* Does not use images with appropriate aspect ratio. (In all fairness, the difference between the actual image aspect ratio and the displayed aspect ratio is less than 10%. And because I'll be re-creating this website using the same images and display size specifications, I fully expect that my copy will suffer from this same issue.)

Now, just for fun, let's run the original website through an code validator!

[Here's the original website](https://validator.w3.org/nu/?doc=https%3A%2F%2Fwww.jeep.com%2F)

## Project

I've gone ahead and made a few modifications to the copy I built as I saw fit. Among them are the following : 

* Built a simple robots.txt. There's not a lot to see here, this is mostly a spec-compliance thing. 

* Includes web manifest. I put together a simple manifest JSON to allow this website to run as a PWA for mobile devices. 

* Added `Noscript` tags. It's important to notify the user if JavaScript is disabled.

* Boost chevron size for dropdown menus and clickable links. The original chevrons appear a font-size or two smaller than the text they're referencing. The original website also appears to, for whatever reason, use several different sizes of them. I decided to standardize and enlarge them a bit to make them stand out more. For reference (screenshotted at different screen resolutions, so padding may differ) : 

Original Header : 
![alt tag](./imagesForReadme/chevron-original.png) 

My Header  :
![alt tag](./imagesForReadme/chevron-copy.png)

* Change carousel buttons. The original website uses a different gliphycon set than I have with Bootstrap. Their carousel buttons, when hovered over, also cast a shadow that does not extend to the bottom of the image carousel. It's a minor bug in the website, and one I had no intention of replicating. I opted instead to use the Bootstrap default carousel buttons (although I did modify them a bit to boost visibility and styling). For reference : 

Original Button : 
![alt tag](./imagesForReadme/carousel-original.png)

My Button : 
![alt tag](./imagesForReadme/carousel-copy.png)

* Use only Roboto font at 400/700 weights. The original website uses a mixture of fonts and weights. Including Proxima Nova headers, which unfortunately are not free or open source. On the upside, My website will have one less resource to reqest!

* Changed a few glyphicons. I was told to use bootstrap, so I'm sticking to bootstrap and FA icons. Which means I've had to make a few substitutions. They're minor, but worth a mention.

Original Info Disclaimer : 
![alt tag](./imagesForReadme/info-original.png)

My Info Disclaimer : 
![alt tag](./imagesForReadme/info-copy.png)

Original Search Bar : 
![alt tag](./imagesForReadme/search-original.png)

Copy Search Bar : 
![alt tag](./imagesForReadme/search-copy.png)

## Tests

Lighthouse Audit.

I'm running this test off of the same computer as before. Here are the results for GitHub Pages (scores higher runing on a local server, but a local server is hardly a good representation of reality):
[alt tag](./imagesForReadme/gh-pages-lighthouse-scores.png)

Network Audit.

[alt tag](./imagesForReadme/gh-pages-network-metrics.png)

[And here's my deployed GH-Pages copy run through a html validator. It's still not perfect, but much improved over the original.](https://validator.w3.org/nu/?showsource=yes&showoutline=yes&showimagereport=yes&doc=https%3A%2F%2Fmultishifties.github.io%2Fjeepfrontpage%2F)

## Thoughts

Done over again, I'd make better use of bootstrap mobile visibility classes instead of rolling my own utility class names for custom breakpoints. Bootstrap engineers have already taken this into account. And if I had to roll my own, I'd separate any sizing utility classes into a separate file for specificity if I for whatever reason needed my own custom breakpoints.

It's challenging to duplicate a website when the website itself is constantly seeing improvements and bug-fixes. I've noticed several changes throughout the website that were definitely not there when I first began duplicating this website. Also at some point you have to make a decision to either stick to creating as exact a copy of the original as possible, or choosing to modify or improve certain elements. I've pointed these changes out where I've diverged from the original spec.

As a random and interesting aside: because the original website uses google analytics, and because I've gone from never seeing this website before to visiting it as often as what feels like 100 times a day, every single website I go to now is trying to sell me a brand new 2018 Jeep renegade. I imagine this will keep up for a few weeks at least.

When designing mobile first, it's easy to overlook progressive enhancement opportunities that having a mouse can bring. When you're analyzing a website in a mobile emulator, all :hover pseudo-class rules are ignored because there is no :hover on a mobile device. Remember to un-dock your design every now and then. It can prevent you from having to go back over your entire design to re-add all the hover functionality for desktop and laptop users. (Ask me how I know...)

Sadly, I wasn't able to add all the pop-up/drop-down menu functionality into this website without significantly overshooting my self-imposed 1 business week deadline for this project. If I had more time, I'd definitely add more interactivity to the website. As it is now, I have a JavaScript file being linked in that serves no purpose because I didn't have time to build the extra functionality in.. 

## Production

As a reminder, the focus of this project was on duplicating an existing layout and UI as a demonstration. As such, it's not configured with continuous development in mind. But if it were I'd probably do the following:

Minify assets as an npm script. Minification of assets, tree-shaking bootstrap for smaller file size, etc would all be nice to have if this was a full-blown website that would see regular changes. 

Probably use a view engine. This would help a lot when you have sections you want to re-use between pages. 

## Bonus

And if you've just read this entire thing, here's the outline and draft of the website I sketched on some scrap paper before I began building it. (Please, pardon the handwriting. I studied through school entirely on computers)
[outine doc](./imagesForReadme/outline-draft.pdf)
