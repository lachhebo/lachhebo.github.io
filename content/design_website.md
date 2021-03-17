---
layout: post
title: 'designing a lighweight   blog using github pages, zola and ovh'
date: 2021-03-14
published: false
---

This blog is actually quite old, the first version was created in 2019, but I recently felt the need for using a more lightweight blog. This urge is probably caused by the recent trend for **minimalism**, as websites bloated with animations actualy don't impress me anymore.

'*Perfection is reached not when there is nothing more to add, but when there is nothing more to remove.*'
Antoine de Saint Expuréry.

The size of a webpage increased by 3x in the last 10 years in average, meaning slower surf speed for users, more memory and CPU consumption, this incentivize users to buy new hardware more quickly. As a consequence, the carbon impact of poorly designed website is not negligible.

Besides, I want to use simpler tools, so that I may have a better grasp of my actions at the lower level. Also, I want a custom domain name as well as a comment fonctionnality.

## Finding a better SSG

Over the last years i have used [jekyll](https://jekyllrb.com/). It is a great tool that works well with Github (developed by the Github team). Yet, I was never quite satisfied with jekyll. Because Jekyll is written in Ruby (btw not a performance oriented language), I had to deal with dependency management. Moreover, jekyll seems to use too many abstractions for a simple blog.

The first alternative to Jekyll I wanted to use was [ssg5](https://www.romanzolotarev.com/ssg.html), a SSG written in posix shell, to use it with markdown posts, I installed a C library (lowdown) on my system. ssg5's codebase is quite small (less than 1000 lines of code) but it **wasn't rigorously maintained**. Hence, it was not compatible with the latest version of lowdown, the C library used to handle markdown file.

Hence, I looked at [makesite.py](https://github.com/sunainapai/makesite), a small python script (130 lines of code) which handles everything for the users. Makesite is a very good solution that will satisfy most users. The code serves as documentation and the users can easily understand how makesite works. However, I wanted to try a similar tool, written with another language.

Eventually, I ended up using [Zola](https://www.getzola.org/), a SSG written in rust. It comes as a simple binary executable (no dependencies), is simple (in both lines of code and in usage) and it has a great documentation. Last but not least, it feels much more **snappy** than Jekyll.

## Creating a simpler website

The key to create a lightweight website is to :

- remove all javascript
- having the smallest amount of css involved

I have choosen to start from a theme called **lightspeed**, which is optimised to be as lightweight as possible. I did a bit of configuration over it and my website was ready.

Using OVH, I bought the domain name *'ismael.lachheb.com'* instead of using the Github default one with OVH. I set up the DNS with *A name* using the github servers' addresses (185.199.[108-109-110-111].153).

<img height="350" src="https://raw.githubusercontent.com/lachhebo/lachhebo.github.io/screenshots/ovh_dns_show.png" />

It was not enough for my website to correctly works. Every time a new article was published to the website. Github was serving the website to the address *lachhebo.github.com*, the default address and not my custom domain name. Eventually, in the repository, I fixed this issue by adding a CNAME file containing the name of my website *ismaellachheb.com*.

Last step, to allow users to write comments on the blog, I did not want to use a server to save the comments. The simplest solution I found using open source solution was to use [utteranc.es](https://utteranc.es/). It allows user to publish comments on my blog using their Github account. It uses javascript to scrap the data from the Github API.

This small script is enough to link the Github repository containing the comments to my website.

```javascript
<script src="https://utteranc.es/client.js"
        repo="lachhebo/lachhebo.github.io"
        issue-term="title" 
        theme="github-light"
        crossorigin="anonymous" async>
</script>
```

Actually, each article is automatically linked to an issue with my blog github repository. As I think most people looking at my dev blog will have a github account, I think it is a great idea.

At the end of the day, I am really happy with the result ! 🥳
