---
layout: article
title: Why Jekyll? Leaving Webdev behind
show_edit_on_github: false
tags: personal 
subtitle: A big test
aside:
    toc: false
---
### From Ruby, to Node.js, to Github pages

TL;DR - Who can be faffed with administrating infrastructure, developing with bulky JS frameworks, and managing deployments? Jekyll on github pages is free, lightweight, and takes my focus off Webdev and back onto writing.

---

I deployed the [first build of my website](https://jamalrahman.co.uk/website-v1/) during the first term of my first year as a CS student at University back in 2015. You'll notice that I landed on my current colour scheme rather quickly (correct as of time of writing).

![](/assets/images/2021-01-25-website-journey/v1.jpg)

You'll also notice how I wrote about aspiring to be a full stack web developer. Although I didn't actually know the term 'full stack web developer' at the time, so I just generalised to sell myself as a miscellaneous Web Developer! *Hire me now!*

### Why even have a website?

The full-screen landing page, the flashy auto-typing intro, and the autoscrolling navbar-links all make sense with the context in which the website was built. The entire project was an endeavour in devloping my full stack webdev skills (HTML/CSS/JS + some backend), as well as understanding basic deployment & sysadmin principles. And not just that; the entire project was also built to *demonstrate* such a skillset to a potential employer. Everybody knows the impact a strong suite of side-projects can have on the career prospects of a graduate seeking to find a CS career.

### Frameworks & Deploying

From 2015 right until 2021, I deployed my website on the cloud computing provider, [DigitalOcean](https://www.Digitalocean.com). 2015 was before the time of widespread ad-hoc serverless computing, so I provisioned an Ubuntu 16.x VM and deployed my application behind Nginx for routing.

The project lived as a Ruby on Rails app and used jQuery for most of the frontend. Yes, that's how well you can date this version of the website. Rails + jQuery.

By second year of my undergrad I realised that tech wouldn't cut it and ported the website to Node.js. It was then that I came up with the design and templating system for [the website that carried me from 2017 to the end of 2020](https://jr-nodejs.herokuapp.com/).

![](/assets/images/2021-01-25-website-journey/v2.jpg)


While the design of this v2 website still slaps, it fits the wrong purpose. As before, it stood as an example of full-stack web development, UX design, and showing my familiarity with wider software engineering tooling: unix competency, working with cloud platforms, deplyoment processes.

It was around this time that I started wanting to write more and web-dev less, and I first used proxied `blog.jamalrahman.co.uk` to redirect towards a version of the 'Ghost' blogging platform that was deployed on my cluster. Unfortunately I lost the contents of this blog somewhere down the line.

### 2021 and beyond

I'm now a few good years out of University; my need to demonstrate a full-stack engineer skillset is far lessened, and my desire to keep up with DIY-maintaining a Ubuntu VM & keeping up with Node.js is all but dead. To be blunt, I spend my day job deploying ML behind well-architectured web apps, I don't want to fuss with that stuff when I get home (or log off the work laptop. #justLockdownThings). I just want to write, and share knowledge!

## Github Pages & Jekyll

I made the decision to get rid of the flashy 'portfolio' style and point my domain to a simple static blog. Fortunately for me, Github has incredible native support for **free, hosted** blogs using Jekyll and Github pages. It really removes all the fuss and allows me to write using simple markdow.

There are a couple of ways to get started with Jekyll & Github pages:
1. Instantiate a clean Jekyll project locally. Push up to a repo at `github.com/username/username.github.io.git`
2. Fork a pre-edited Jekyll theme, pull locally and make necessary changes.

Details on setting up a Github pages site with Jekyll can be found here:
* [https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll](https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyl)
* [https://jekyllrb.com/docs/github-pages/](https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyl)

After setting up Jekyll and starting an initial blog, I opted to start again by forking from the [Jekyll TeXt theme](https://github.com/kitian616/jekyll-TeXt-theme), which gave me a good basis upon which to tailor the blog's Sass & CSS for my own color & font scheme.

Thanks to the power of Jekyll, I can focus on delivering content, and save the focus on building a backend for my 9-5.