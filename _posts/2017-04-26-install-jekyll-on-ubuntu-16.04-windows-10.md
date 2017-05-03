---
title: How to install Jekyll on Ubuntu 16.04 or Windows 10 - A Step-by-Step Guide
date: 2017-04-26T11:00:00+00:00
author: wiseindy
comments: true
layout: post
header:
  image: /assets/images/featured/featured-jekyll-full.jpg
  teaser: /assets/images/featured/featured-jekyll.jpg
categories:
  - IT
tags:
  - jekyll
  - jekyllrb
  - ruby
  - ruby2.3
  - ubuntu 16.04
  - ubuntu 14.04
  - ubuntu
  - guide
  - linux
  - ubuntu
  - static
  - static site generator
  - Guides
---

This guide will show you step by step how to install Jekyll 3.4.3 on a machine running Ubuntu or Windows 10.
[Jekyll's official guide](https://jekyllrb.com/docs/installation/) is good, but it's very basic and doesn't explain how to install Ruby, RubyGems and other dependencies.

<!--more-->
## What you need:

* An Ubuntu 16.04 or Windows 10 system. This guide should also work for older Ubuntu 14.04
* And as always, an internet connection

## Step 1:

Skip to step 2 if you're installing Jekyll on Ubuntu.

To install Jekyll on Windows 10, we need to first enable **Windows Subsystem on Linux**. [Here is a detailed guide that will show you how to do this step-by-step.](/it/enabling-linux-bash-shell-in-windows-10/)

## Step 2:

We will now install **ruby2.3**. To do so, we have to first add the brightbox repository. When asked whether you want to confirm adding the repository, hit ENTER to proceed.

```shell
sudo apt-add-repository ppa:brightbox/ruby-ng
sudo apt-get update
```

Install **ruby2.3**

```shell
sudo apt-get install ruby2.3 ruby2.3-dev
```

Now you should have **Ruby** and **RubyGems** installed which are the prerequisite for installing Jekyll.

<div class="row">
  <div class="col-12">
    {% include adsense-post-content.html %}
  </div>
</div>

## Step 3:

Install [GCC](https://gcc.gnu.org/install/) and [Make](https://www.gnu.org/software/make/)

```shell
sudo apt-get install gcc make -y
```

## Step 4:

Install Jekyll and Bundler gems

```shell
sudo gem install jekyll
```

Guess what? That's it. You have Jekyll 3.4.3 installed.

## Further information:

Here are some commands from [jekyllrb.com](https://jekyllrb.com/docs/quickstart/) that should get you up and running with a new blog.

```shell
# Create a new Jekyll site at ./wiseblog
jekyll new wiseblog
```

To build this site:

```shell
# Change into your new directory
cd wiseblog

# Build the site and preview it
bundle exec jekyll serve
```

**Note:** If you're running Windows, you may get an error when you try to run `bundle exec jekyll serve`. In this case, simply run it with the `--force_polling` option as follows:

```shell
bundle exec jekyll serve --force_polling
```

Now you can preview your website on `http://localhost:4000`

## Notes:

(You can skip this part. This is only for my reference and for anyone who faces a similar issue)

I had to install [Nokogiri](https://github.com/sparklemotion/nokogiri) for my site and was having issues. This is how I solved it.

Below are the installation instructions on [nokogiri.org](http://www.nokogiri.org/tutorials/installing_nokogiri.html):

```shell
sudo apt-get install build-essential patch
sudo apt-get install ruby-dev zlib1g-dev liblzma-dev
sudo gem install nokogiri
```

(header image source: [jekyllrb.com](https://jekyllrb.com))
