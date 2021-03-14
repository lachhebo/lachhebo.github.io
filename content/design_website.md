---
layout: post
title: 'designing a lighweight   blog using github pages, zola and ovh'
date: 2021-03-14
published: false
---

This blog is actually quite old, The first version was created in 2019, but i recently felt the need for using a more lightweight blog. This urge is probably caused by the recent trend for **minimalism**, website with bloated with animations actualy don't impress me anymore and I feel like less is more.

The size a webpage increased by 3x in the last 10 years, it means slower surf speed for users, more memory and cpu consumption, this incentivize users to buy new hardware more quickly. Hence, the carbon impact of poorly designed website is not negligable.

Last but not least, I want to use simpler tools, have a better graps over what I'm doing at the lower level, and add a custom domain name and comment fonctionnality.

## Finding a better ssg

Over the last years i have used [jekyll](https://jekyllrb.com/), it is a pretty great tool, it works well with Github (develop by the Github team). Yet, I was never quite satisfied with jekyll. Because Jekyll is written in Ruby (btw not a performance oriented langage), I had to deal with dependency management. Moreover, jekyll seems to use too many abstraction over a simple website written with html/css/js.

The first alternative ssg I wanted to use was [ssg5](https://www.romanzolotarev.com/ssg.html), a sgg written in posix shell, to use it with markdown posts, I installed a C library (lowdown) on my system. ssg5's codebase is quite small (less than 1000 lines of code) but it **wasn't rigorously maintained**. Hence, it was not compatible with the latest version of lowdown, the C library used to handle markdown file.

Hence, I looked at [makesite.py](https://github.com/sunainapai/makesite), a small python script (130 lines of code) which handle everything for us. makesite is a very good solution that will please most people. The code serves as documentation and the users can easily understand how makesite is working. However, as I am working 40h a week with python, I felt like I would like to use a tool written with another langage.

Eventually, I ended up using [Zola](https://www.getzola.org/), a ssg written in rust. It comes with a simple binary (no dependencies), is simple (in both lines of code and in usage) and it has a great documentation. Last but not least, it feels much more **snappy** than Jekyll.

## Creating a simpler website

The key to create a lightweight website is to :

- remove all javascript
- having the smallest amount of css involved

I choosed to start from a theme called **lightspeed**, it was optimised to be as lighweight as possible. I did a bit of configuration over it and my website was ready.

The, I bought my domain name instead of using the Github default one with OVH. I set up the dns A name using the github servers, and in the repository, I added a file contaning a CNAME.

Last but not least, to allow users to write comments on the blog, I did not want to use a server to save the comments. The simplest solution I found using open source tech was to use [utteranc.es](https://utteranc.es/), it allows user to publish comments on my blog using their github account. The downside is uses javascript to scrap the data from the github API, I think I can forgive myself.

```javascript
<script src="https://utteranc.es/client.js" 
        repo="lachhebo/lachhebo.github.io" 
        issue-term="title" 
        theme="github-light"
        crossorigin="anonymous" async>  
</script>
```

Actually, each article is automatically linked to an issue with my blog github repository. As I think most people looking at my dev blog will have a github account, I think it is a superb idea.

At the end of the day, I am really happy with the result ! 🥳
