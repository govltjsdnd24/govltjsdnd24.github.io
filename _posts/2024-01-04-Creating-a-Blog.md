---
categories: [ Development , Blog ]
tags: [blogging] 
---

So.. this was my first time creating a blog. I didn't really find any reason to make it before I realized that **I couldn't retain my learning** if I didn't record it. Moreover, I can always return to my documentation whenever I feel necessitated, so that's a plus. Anyways that's how my blog-creating voyage began.


## The Process

I wasn't particularly good with handling CSS. Could be just a lack of skill, or deficit of my endeavor. Either way, I wasn't going to wear myself out by just trying to make a framework for my blog's content. Hence, I resorted to using Jekyll, which is a static website generator that's based on Ruby ( a programming language that's entirely Object-oriented and seems to be have a palpable presence in Japan's financial sectors).

Why did I choose Jekyll? It was one of the most used tool for Github Pages. It looked easy to handle and customize. Many developers distributed their website using it. Hopefully, I don't regret this choice.

I used http://jekyllthemes.org/ website to find a theme to my liking. Many seemed tempting, but Chirpy looked the slickest. 

![jekyll_theme](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/ae1e02a6-1767-4510-98ec-e8bee601ea20)

There seemed to be 2 ways of using Chirpy as my website. 

 1.  Fork it from Github and customize it with Jekyll
  2. Use Chirpy Starter

I was following a Korean blogger's guide on applying the Chirpy theme (https://velog.io/@coastby/Git-GitBlog-Chirpy-Jekyll-Theme-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0), so I tried doing it  in a rudimentary way, which was method number 1. I installed Ruby, Gem, and Jekyll, then forked Chirpy to my repository, finalizing the setup process by removing unnecessary files and customizing the _config.yaml file.
However,  problems began to emerge.

## Troubleshooting

Despite following the guideline and pushing the repository to Github, I could only see the text "--- layout: home # Index page ---" when I connect to the url for my Github Pages. I didn't remember writing such thing in my page. After some exploration, I realized that the aforementioned text was the content of my index.html. However, if correctly set up, Chirpy wasn't supposed to show the text itself, but rather a functional web page. I checked the actions tab from my repository to find out that my build had failed. 

![failed action](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/dc3ce057-7c2b-45e2-8750-f7dd9e92cd87)

Flustered, I searched the internet for enlightenment, and tried the following "solutions":

 - changed the pushing repository to main (originally main and master) from .github/workflows/pages-deploy.yml
 - changed "" to '' in the url section from _config.yaml
 - created another repository called gh-pages and tried pushing the content there
 - re-ran all jobs from the failed builds in the actions tab

However, all of the attempts failed, and I decided to just start from scratch--this time using the Chirpy Starter. I created a new repository, downloaded and unzipped the Chirpy Starter into it and pushed the content. Unfortunately, errors still popped up, but this time it didn't occur in the build phase, but rather the test phase.

![build_failed_detail](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/c8a57dcb-5fa7-43f1-bb0a-84b1c69b8e68)

Problems seemed to be happening because links were not being recognized. I searched for answers but to no avail, and tried fidgeting with the content of _config.yaml myself...

![successful_action](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/8da61797-b378-4af0-b1a1-6f8089e7204f)


Voila! I made it work. It was because the url had http:// rather than https:// inside the _config.yaml file. Such a dumb and elementary mistake... Nonetheless, ultimately, I was able to make my blog work! Through this experience, I realized that...  I have to start working smarter. Seriously..

![chirpy_starter_success](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/55ce54a1-7f19-470f-ba64-871f337a387a)
