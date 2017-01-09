---
layout: post
title:  "Blogging with GitHub Pages and Jekyll"
author: Ed
date:   2017-01-05 14:00:00
excerpt: "How we got this blog up and running with GitHub Pages and Jekyll."
---
Since we are fairly new to [Jekyll](http://jekyllrb.com/) and [GitHub Pages](https://pages.github.com/), I thought I would take a few minutes to discuss our experience with the platform so far. As I mentioned in the [first blog](https://hypraptive.github.io/2017/01/02/welcome-to-hypraptive.html), we decided to go down this path after reading Andrej Karpathy's blog [Switching Blog from Wordpress to Jekyll](http://karpathy.github.io/2014/07/01/switching-to-jekyll/). Andrej's post list some of the reasons for using Jekyll rather than other blogging platforms, and he provides a good example of a work flow. His blog is simple and clean, so I figured I could do something similar. While it's pretty straight forward, I did encounter a few bumps along the way.

I wanted a blog for [hypraptive](https://hypraptive.github.io/), not for myself. So the first thing I did was set up a [GitHub organization for hypraptive](https://github.com/hypraptive). This will serve as our git repository for any open source projects we work on, including the deep learning project I have started to describe. It also allows us to take advantage of the free hosting from [GitHub Pages](https://pages.github.com/) for a blog
at [hypraptive.github.io](https://hypraptive.github.io/). All I need to do is create a repository called hypraptive.github.io and fill it with the necessary Jekyll files. GitHub Pages will do the rest.

### GitHub Pages Setup

To set up the blog, I started following the instructions on the [GitHub Pages](https://pages.github.com/) site. It's a quick process, but I soon found out what I ended up with was a single page site with no concept of blog posts. I thought about starting to edit all the files to build up to a blog, but I figured it should be easier. I ended up deleting the repository and starting over. The important thing I learned from this process is how to enable GitHub Pages. In the settings for the repository, theres a section labeled GitHub Pages. This section contains some relevant settings for a GitHub hosted page. You can even set up a custom domain.

### Installing Jekyll Locally

I looked at a few blogs to see how they got started, but the problem is, the process changes as Jekyll changes. So I decided to follow the [Jekyll Quick Start Guide](https://jekyllrb.com/docs/quickstart/). Actually, I started out with the [Installation Guide](https://jekyllrb.com/docs/installation/). Fortunately, I already had all of the prerequisites on my MacBook Pro (Ruby, RubyGems, NodeJS and Python 2.7). Installing the Jekyll gem is a simple command, but as I was creating my new site, I realized I missed the step about installing [bundler](https://rubygems.org/gems/bundler). As the time I'm writing this post, the default theme makes use of bundler, which wasn't the case earlier on. This is an example of the kind of changes to watch out for in any open source project (it is also why I am not including all the command lines).

Once I realized I needed bundler, I ran into my next problem. During one of the steps I started getting an error related to a specific version of [nokogiri](https://rubygems.org/gems/nokogiri).

```
Gem::Installer::ExtensionBuildError: ERROR: Failed to build gem native extension.
[stuff deleted]
An error occurred while installing nokogiri (1.6.8.1), and Bundler cannot continue.
```

After much searching and multiple attempts, I was finally able to get around this problem (at least in my specific case) with:

```
sudo ARCHFLAGS='-arch x86_64' gem install nokogiri:1.6.8.1 -- --use-system-libraries
bundle install
```
After that, I was able to start the local server built in to Jekyll using `bundle exec jekyll serve`. I started by adding the [Welcome post](https://hypraptive.github.io/2017/01/02/welcome-to-hypraptive.html) and made sure that was working locally. If you're not very familiar with markdown, check out this [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) for the basics.

### Pushing to GitHub

Once I had a functional local version of the blog, I added it to GitHub. I kind of like GUI tools, so I'm using [GitHub Desktop](https://desktop.github.com/). I use it for all my commits, and don't forget to `sync` when when you want to push it to GitHub! If you created the repository locally, make sure check the settings on GitHub to enable GitHub Pages!

### Adding Disqus Comments and Google Analytics

I wanted to add comments and traffic tracking to the blog. It turns out the default theme, [minima](https://github.com/jekyll/minima), already has these features built in, you simply need to enable them.

For [Disqus](https://disqus.com/), you need your Disqus `shortname`. I already had a Discus account which I have used for commenting, but I didn't have any discussions. From my Discus settings, I was able to add a new site for hypraptive.github.io. I enabled it on the blog by adding the following to the `_config.yml` file (where in my case `my_disqus_shortname` is `hypraptive`):

```yaml
  disqus:
    shortname: my_disqus_shortname
```
This was not working for me at first. After some digging, I ran across [Ian Goodfellow's post](http://www.iangoodfellow.com/blog/disqus/jekyll/2016/11/22/adding-disqus-to-jekyll.html) and found my problems. I needed to properly set the `url` variable (in my case `url: "http://hypraptive.github.io"`) in `_config.yml`. I also had to add `hypraptive.github.io` to the Trusted Domains for the site on Disqus (it's under Advanced settings). It took a few minutes to propagate, but then everything started working.

The default theme also supports [Google Analytics](https://www.google.com/analytics/). To enable this feature, you need to register you site on Analytics and get a tracking ID. Then simply add the following to the `_config.yml` file (using your own tracking ID which starts with `UA-`):

```yaml
  google_analytics: UA-NNNNNNNN-N
```

### Wrapping Up

That's pretty much where we are today.

Aside from blog content, there are a few more site improvements I would like to make. To keep track of these ideas, we started using GitHub's new [Projects](https://help.github.com/articles/tracking-the-progress-of-your-work-with-projects/) feature. It enables you to set up a simple workflow to prioritize and manage notes (which we're using like simple stories), issues and pull requests. We're using this basic flow for the blog:

* **Backlog:** Prioritized list of stories/epics, issues, etc.
* **In Progress:** What we're currently working on
* **Done:** What we have completed and deployed

Here's our basic [Site Improvements Project](https://github.com/hypraptive/hypraptive.github.io/projects/1). I haven't bothered creating any issues so far, but I'm sure the need will arise at some point.

That's about it for now. We will get back to the deep learning project in the next post.
