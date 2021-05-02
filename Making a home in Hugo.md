A few years back I spent a good bit of time with Jekyll, a static-site generator that is compatible with github-pages. Static-site generators have fascinated me every since. I work professionally with Magento, which takes a lot of effort to host well. With something like Jekyl or Hugo, the infrastructure needs reduce dramatically as you only need to serve a few html files ultimately. I'm also a giant devops geek, so I always jump at the chance to build some continuous delivery workflows.

## A little History...

A few things have changed since the last time I worked on this blog. Back in the day, Github Actions didn't exist, so your ability to heap features onto Jekyll were limited. This led me to using Netlify to do my building and hosting, which honestly was fine. I event learned a little ruby along the way. But times change... we can use actions to use any tool we want to populate github.io. I also don't want to spent a lot of time with a four-year-old tool and repo, so I looked into what the kids were using. I played with a few options, and Hugo really stood out.

## Why Hugo?

First, Hugo is _fast_. Github actions are completing in 5-10 seconds. This is as close to real-time as I need, especially coming from a world where Bitbucket Pipelines or Netlfy builds take a minute before they even start! 

Second, it's really simple. Probably the one thing that convinced me to go with it is this [Hugo Example Repo](https://github.com/gohugoio/hugoBasicExample), where there's no theme files - just the meta files. While this level of separation is important to me, I actually wanted to completely de-couple the content  from the rest of the codebase, and this didn't go far enough, but it's nice that Hugo likes git submodules because this made going all the way fairly easy.

Third, I like how customizable it is. It supports widgets (blocks you can move around), it supports like four varieties of config files. While most of these static site generators support markdown, this will take many files you throw at it, and it's markdown files don't need grey-matter, which I found is a barrier to blogging that mostly stopped me.

## Architecture

Like I mentioned earlier, I'm using a github action to run the hugo build and populate the gh-pages branch which gets served by github.io. I was able to find an action file that does this out the box, but I modified it to run `git submodule update` so that it pulls in the latest content from my blog repo. I also added a RepositoryDispatch trigger, and in my blog repo I added an action that triggers it I can deploy by updating either repo. 

## Content Management

This is where I felt my Jekyll instance fell short. I tried using Prose and Forestry, and this week I looked into Netlify CMS to find some frontend to manage this well. But of course, the whole draw of markdown is supposed to be how ambiguous it is. The problem is that with my Jekyll site, you needed a bunch of custom front-matter. This meant you needed a frontend that managed the grey-matter, which meant you were screwing with that the whole time.

The front-matter problem also had me take a long-hard look at what I'm tracking, and make some executive decisions about the data I track. I decided that, by default, I'd prefer not to have any front-matter, that an empty markdown file with just content should post. This took a few template tweaks, but was not hard. I even went so far as to have it prefer the filename for the title field (you will notice my filenames contain caps, spaces, some special characters). This seems to work, and from a style stand-point makes it very obvious on how to create content. Just removing friction. To this end, I choose a template that requires little to no imagery, this will be a text based blog moving forward primarily. 

In other parts of my life, I've started using [Mark Text](https://marktext.app/) as a general-purpose note taking app, where my ~/Documents directory just has directories-upon-directories of markdown files. This is easy to maintain, it's great. So with this, I've cloned `superterran/blog` to ~/Documents, and I added a script `~/bin/publish` that commits the contents and pushes it up.

```bash
#!/bin/bash
cd ~/Documents/Blog
git pull
git add .
git commit -m "publish command ran on $(whoami)@$(hostname) on $(date)"
git push
```

## Conclusion

So far, I think it's great. The builds are super-fast, the content is well separated from the app, the hosting is free, and everything is built around markdown. What's not to like? If you want to learn more or check under the hood, check it out on [GitHub](https://github.com/superterran/superterran.github.io)!
