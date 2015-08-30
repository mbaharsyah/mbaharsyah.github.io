---
published: false
---

---
layout:     post
title:      Building Static Website
date:       2015-08-30
summary:    How I use Jekyll and Github Pages to build a website and publish it in my own domain.
categories: web
---
![website](http://www.wedholmab.se/wp-content/uploads/2013/04/webbutveckling-1.jpg)

As described in [Previous Post](http://www.mbaharsyah.xyz/general/2015/08/27/new-website/), I built this website using Jekyll, hosted on Github Pages and use domain name registered from namecheap. This is how it was done.

## Github Pages

I used my existing Github [account](https://github.com/mbaharsyah) and created a new [User Pages](https://help.github.com/articles/user-organization-and-project-pages/#user--organization-pages). Initially I only created a repository "[```mbaharsyah.github.io```](https://github.com/mbaharsyah/mbaharsyah.github.io)" and added an ```index.html``` file using Github's web interface with "Hello, World!" text.

![2015-08-30-add-gh-file.png]({{site.baseurl}}/images/posts/2015-08-30-add-gh-file.png)
{: .centered}

Then I verified that everything was working properly by browsing to https://mbaharsyah.github.io/. Saw my "Hello, World!", and the ```index.html``` served its purpose. So I deleted the file and the repository to prepare for the real action.

## Jekyll

### Installation

I installed Jekyll on my Mac, and the process was pretty straight-forward  even for me with zero knowledge of [Ruby](https://www.ruby-lang.org) (Yes, it requires Ruby to run Jekyll). For Windows, though, one needs to install Ruby and some other dependencies first. But one still can follow the instruction [here](http://jekyllrb.com/docs/windows/#installation)

Follow these instructions to install Jekyll on a Mac

1. Install XCode command line tools
   Some of the Jekyll dependencies depend on XCode command line tools, to install it run following command through terminal:
   {% highlight sh %}
   xcode-select --install
   {% endhighlight %}
   and follow the instruction in GUI
2. Install Jekyll using [RubyGems](https://rubygems.org/) by running this command in terminal:
   {% highlight sh %}
   gem install jekyll
   {% endhighlight %}
   It will start downloading some dependencies, and when everything is finished, you're set to run Jekyll locally on your machine.
 
### Creating a Website

There are several ways to create a new Website using Jekyll:

1. Ask Jekyll to create it by running following command:
   {% highlight sh %}
   jekyll new blog
   {% endhighlight %}
   After completed, it will create a new folder ```blog``` in your current directory. It also create a structure required for your website

2. Download available templates
   There are tons of [great templates](http://jekyllthemes.org) out there which you can [use](https://github.com/jekyll/jekyll/wiki/Sites). Most of them (if not all) can be downloaded to your local machine for your own use.
   
3. Fork and Clone an existing Jekyll Github Pages Site / Template
   I recommend this method, and this is what I did. I decided to use [Pixyll](http://pixyll.com/) theme and forked their github [repository](https://github.com/johnotander/pixyll) and renamed it according to github pages rule (i.e. ```<username>.github.io```
   And then I cloned this repository into my machine:
   {% highlight sh %}
   git clone https://github.com/mbaharsyah/mbaharsyah.github.io.git .
   {% endhighlight %}

### Updating the Website

After creating the Jekyll website, you need to modify some [configurations](http://jekyllrb.com/docs/configuration/) located in ```_config.yml```. This normally includes the website's name, author, and other information according to the template that you use.

### Running the Website locally

After all configurations are set, all [posts](http://jekyllrb.com/docs/posts/) are reviewed, updated, deleted or added. You want to see how the website looks like. You can run it on your local machine by running following command
{% highlight sh %}
cd blog
jekyll serve .
{% endhighlight %}
It will trigger your site to be built and when it is done, browse to http://localhost:8080 to see your website.

### Publishing to Github Pages

When you're ready to publish your website on Github Pages, you can commit all your files to Github repository (```<username>.github.io```). If you created the website like in option 3 above, you can do it by running:
{% highlight sh %}
git add --all
git commit -m "Publishing my website to Github"
git push origin master
{% endhighlight %}
It will upload all your modifications to the repo and then you can open http://<username>.github.io to see your website.

If you use the other methods to create your website, you may want to see github [help page](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) on how to perform initial push to the repo

## Custom Domain

When everything is working fine with your website running on http://<username>.github.io, you can then link it to your own [domain name](https://en.wikipedia.org/wiki/Domain_name). I use namecheap as my [Domain Name Registrar](https://en.wikipedia.org/wiki/Domain_name_registrar), but this guide shall be generic enough for all others.

### Add CNAME file in repository

Using the same way as ```index.html``` file above, create a file named ```CNAME``` (all in caps) which contains single line which is your domain name, e.g. 
<pre>
www.example.com
</pre>

### Modify DNS Settings

From your domain control panel, find DNS settings or hosts record. For namecheap it's under My Account --> My Domains --> Manage Domains --> All Host Records.
Create 2 [A records](https://en.wikipedia.org/wiki/List_of_DNS_record_types#A) pointing to github addresses:
<pre>
@ 192.30.252.154 
@ 192.30.252.153
</pre>

In general, it means that any request to your domain name, must be forwarded to either of those DNS (they're Github's, btw). And then it's Github's task to point it to the correct website.

You need also to add a [CNAME](https://en.wikipedia.org/wiki/CNAME_record) entry
<pre>
www <username>.github.io.
</pre>

What it means is that www.<yourdomain> points to <username>.github.io. You can of course change www to any subdomain you would like to have. And please note there's a full stop at the end of github.io domain. See below for my complete setup in namecheap

![2015-08-30-dns.png]({{site.baseurl}}/images/posts/2015-08-30-dns.png)

