+++
author = "Brayden Winterton"
categories = ["Code"]
date = "2016-10-25T21:27:01-06:00"
description = "My journey to find a better blogging tool"
featured = ""
featuredalt = ""
featuredpath = ""
draft = false
title = "Giving Up the Ghost"

+++

Up until recently (about a week ago), I was running this blog on the [Ghost](https://ghost.org) blogging platform in a self hosted environment. Ghost really has always served me quite well, I don't realy have much to complain about, other than the odd lack of some markdown features that I missed. I wasn't particularly looking to get off of Ghost at any point, rather, the idea just struck me out of the blue. I realized that there were quite a few good static site generators out there; things like Jekyll, Hugo, Hexo, Octopress, etc, had started to become more and more popular. This sparked the idea that I could really run quite a few things on static site generators like these and not have to worry about maintaing servers, software, patches, and all the other enjoyable sysadmin work that comes along with those things. However, like many a good idea, it didn't get the time or attention it deserved and the idea quickly moved from the front of my mind back into some little box somewhere in a corner. Several months went by without thinking much about it. Each time I opened my blog or started to draft some new post it would be re-awakened and called to memory. Finally I decided to actually dig in and do some investigation about the feasibility of switching away from Ghost. 

### Why?

Why was I looking into a new blogging platform? Well, I have already touched on a couple of the points, but it really boiled down to a few things in particular:

 * Security/Maintainability of the platform (updates, etc.)
 * Ease of deployment
 * Community
 * Scalability
 * Cost
 
I want to touch on each of these points a little bit and explain the pain points that I was trying to solve. Again, I really hadn't experienced any _major_ pains with Ghost, but there were some things that didn't quite fit my desires and needs. 

First off was the security and maintenance aspect. This was by far the single most important factor in my determination to switch. At this point of my investigation my blog was running on an outdated version of Ghost and the underlying OS had also been neglected for quite some time. Do I have a problem with administrating servers and software? Absolutely not! It is something that I do regularly between work and my personal projects. It is also something that I am very familiar and comfortable with. However, having one less server to maintain and keep track of? Yeah, I would definitely be ok with that :thumbsup:! Being able to run my blog off of static files would allow me to easily run the site off of something like AWS S3 which eliminates my need to maintain a server. This sounded like a dream come true and a much desired outcome of my switch. 

Another issue that I wanted to solve was the ease of deployment. Ghost is easy enough to deploy the first time, however, sometimes updates require some tweaking of files, or copying over specific directories. The updates are fairly consistent, but not always 100% the same. This makes scripting updates and things of that nature difficult, meaning more man-hours put into maintaining the site. New posts however were quite easy to deploy, just simply click publish and your blog is updated! I wanted to maintain the ease of publishing new posts, while also bringing ease to updating themes and other underlying software. The end result being that I could completely automate posting, updating, and theming my 'production' environment. 

Community was a simple requirement; the Ghost community seemed fairly active to me, and that was something I wanted to maintain in my switch. I wanted to find a community that was driven to consistantly improve their product and was willing to communicate well with their users. Having a nice theming community definitely wouldn't hurt either. 

Scaling and cost were much less important than the other three requirements, but they were still on my mind. I wanted my blog to be able to scale easily and quickly in the off chance that one day my blog happens to go viral because of something I posted. I would like the same site that was accommodating my normal low traffic to be able to handle high bursts of traffic. Obviously Ghost scaled to a certain point, but was constrained by the limits of my server. However, a static file server would be much more scalable and would use up less CPU and memory. Especially using something like S3 would allow me to scale at tremendous speed and essentially never worry about my site going down. Cost also played into this as more of an 'added bonus'. Being able to serve up static files out of S3 would lower my cost when there was low traffic and allow me to pay for bursts when they happened to come. So while cost was not a deciding factor in my investigation, it was a nice plus. Who doesn't like saving money? Even if what you are saving is small in comparison to other aspects of life, it feels good knowing you are doing something in a cost effective manner. 

### The Investigation Begins

So what did I investigate, and what did I find? Well, I spent several days pouring over documentation and examples from several different static site generators. In particular I focused my investigation mainly on Jekyll (and it's accompanying plugins like Octopress), Hexo, and Hugo. 

Jekyll is widely known and used thanks to its support on Github Pages. This support on Github has also grown quite the community behind Jekyll. Literally anything you could possibly want to do seems possible with Jekyll. I don't really have any huge complaints about Jekyll, but there were a few minor details that made me not love it as much as some other solutions. For one, Jekyll runs on Ruby. If you know me at all you know that I have a strong disdain for Ruby for several reasons that we don't need to go into here. Biased opinions aside, I don't develop in Ruby, and it's not something I normally run on my machines, as such I didn't want to have to install it just to get Jekyll up and running. It seemed like more effort than it was worth. Another minor annoyance with Jekyll was actually the plugin system. I didn't love the thought of having to keep track of and install plugins in order to easily run my blog. I wanted a generator that 'just worked' and was easy to deal with.

Hexo looked great and seemed to be quite powerful as well. Again, I didn't love the plugin system. I like the power of the plugin system, but I don't know quite how I feel about installing plugins to get things to work. My opinion may change on this down the road, but it's how I feel. The community seemed strong, but not quite what I was looking for. Hexo also felt limiting due to it's blog focused nature. Now, I know you might be thinking, "Ugh! Brayden! You are trying to make a freaking blog! Isn't that exactly what you would want!?", and the answer is "kinda". I was specifically looking to replace my blog, but I would also like to be able to use whatever tool I decided on in the future for other projects. And since I can foresee myself using a static site generator for much more than just my blog, I decided that maybe Hexo wasn't right for me. 

Hugo, however, caught my attention in a big way. First of all, it's written in Go. And again, if you know me, you know that I am a huge advocate for Go. I love it and use it daily in my work. So, I was already a little biased towards this option. However, biases aside, Hugo definitely seemed like the better fit for me. The community is great, and seems to be thriving and constantly trying to improve the platform and the supporting projects. The Hugo team has a goal to make each release faster and leaner than the one before, a goal that I can back 100%! Plus there are a large number of themes for all sorts of things, from blogs to product sites. The theme/templating system in Hugo is extremely intuitive to me (possibly because it is based on go-template) and was something I was able to pick up on in a matter of an hour or two. From everything I could read (before actually getting my hands dirty) Hugo seemed like the perfect fit, so I decided to put it to the test!

### The Benefits

So what were the obvious benefits that I would get by switching from Ghost to Hugo? I tried to answer this question from the outside first, before actually getting into Hugo and trying it out, I wanted to see what benefits I could find just from the documentation and other user's experiences. I came up with a decent list:

 1. No more need to maintain a server, I can run this in S3 (or another static file host) easily!
	* On a side note here, not only could I run this in S3, but Hugo made it super easy to deal with! Several other static site generators didn't make it quite so obvious about the ease of deploying to S3. I think that this was mostly due to their heavy documentation about automated deployments to things such as Github Pages. All of this documentation about these deployment techniques made me wonder if they would easily be able to handle just spitting out the static files for me to stick in S3. 
 * I can version control my blog and keep it in Github (or any other repository)! Which makes it even easier to move around. 
 * Because I can edit static files, I can also edit while I am out of internet service (road trips, camping, etc.)
 * This thing will be super easy to automate in a deployment pipeline, just one command to generate and done! 
 * Deployment will also be made easy because I can just install the binary, no need to worry about installing Ruby, npm, or any other dependencies. 
 * Oooooh! The ability to overwrite any given file from the theme in your own code is awesome! I can edit the theme and keep my edits in version control without having to keep the whole theme in my repo.
 * This just seems super customizable! I can really do a lot with Hugo! 
 * Again, the overwriting theme code with your own is super awesome! Any little tweak I want to make is very simple. 
 * Built in Discus support is really nice as well! 

All of these realizations came solely from reading Hugo's own documentation as well as some scattered user stories found on their own blogs. After digging into the documentation and finding all of these benefits my determination to switch became much more ingrained! What started out mostly as an exploratory effort to see what other kind of options were out there had now become a full blown determination to switch to Hugo. I was getting excited!

### Going Forward

In a future post I will dig into my migration experience as well as my overall experience with Hugo in more detail. If the fact that I am still enamored with Hugo says anything, the migration was actually pretty awesome. 

