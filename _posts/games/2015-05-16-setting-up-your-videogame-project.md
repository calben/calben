---
layout: post
category : games
tagline: "using unreal engine 4 and svn"
tags : [overview, beginner, unreal, setup]
title : Setting Up Your Videogame Project
---
{% include JB/setup %}

* TOC
{:toc}

# Source Control

Git is wildly popular these days, but for videogames SVN is probablby better.
There's also Perforce, but it still isn't completely free.
Theoretically the biggest difference between Git and SVN is the first is distributed and the other is centralised, but for game developmen the biggest difference is SVN keeps track of binary files like 3d models as deltas, keeping them tiny.

You can set up SVN on your own server or you can use one of the services that lets you set up and manage a repository on someone else's servers.

For a more general tutorial than the below, check out tutorialspoint's [article on SVN](http://www.tutorialspoint.com/svn/).

## Install SVN on your own server

If you want a private repository, you'll typically need to pay for it or set up your own server.
I've never used a paid service for SVN, but setting up the system on an Ubuntu machine is easy.
There are tutorials you can look up for doing that, but the gist of it is below. 

{% highlight linenos %}
sudo apt-get install subversion
sudo mkdir /var/svn
cd /var/svn
sudo svnadmin create "newprojectname"
echo "@reboot /usr/bin/svnserve -d --root /var/svn" >> crontab -e
{% endhighlight %}

Then reboot your computer!
SVN will start every time the computer reboots.
Anybody will be able to check in and out code from your repository... that's probably not what you want, so look into making users.
Some tutorials will discuss setting up a firewall and a lot don't.
Occasionally using a firewall can make a lot of problems and headaches with your SVN if you don't do it properly.
If you're not comfortable with setting up the firewall and want to avoid those headaches, you can probably postpone setting up a firewall without anybody trying to hack into your code.

## Create a project on Sourceforge

Sourceforge is amazing, but there are a few pitfalls when using it.
Creating a new project involves 

## Checkout from SVN

Checking out depends on how you set up your SVN.
If you're following a tutorial that does something like the above, then you just need to...

{% highlight linenos %}
svn checkout svn://$SERVER-IP-ADDRESS/my-new-project
{% endhighlight %}


## Checkout from Sourceforge

Sourceforge provides a few ways of checking out, use the `https` method for the easiest experience.
You can also use TortoiseSVN.

For TortoiseSVN, go to the directory in which you want to store your code, then right click, then select "SVN Checkout..."
URL: https://svn.code.sf.net/p/your-project-name-here/code/
Checkout directory: <this will automatically name itself "code" so rename it!>

# Setting up your Unreal Engine project in the repo

Now you have a checked out project! 
Go ahead and make three new directories: "branches," "tags," and "trunk."
Your codebase will go in the "trunk" directory.

Open up the Epic Games Launcher, navigate to "Library" and launch your Uneal Engine.
The opening wizard should pop up and you can make a new project.
Make a new project and select the trunk directoy as its root.

Before updating the repository, you need to add the appropriate directories to the project, like so:

+ Binaries - add this to your repo if you want to include compiled copies of your code.  in svn these will be deltas so it won't get too big, you might as well include this, but it isn't necessary
+ Config - you want this!  add it to your project because it configures your engine behaviour
+ Content - holds your blueprints, textures, etc.  add this.
+ Intermediate - temporary files for building, never add this to your project
+ Saved - includes log files and configuration files.  don't add this.
+ Source - you'll put all your game and engine source here.  add this!  this is the most important folder!

You should also add the uproject file but nothing else.

# Someone else has set up a project

Someone else set up the project, so you don't have to worry about directory structures or anything.
Unless whoever set up the project goofed, in which case you should kindly let them know.
For most projects there will be either a project maintainer or even a small team of technical support.
If you have any trouble, let them know and they should be happy to help out.

## Checking out the code and contributing to it

The checkout process is the same as checking out from Sourceforge above.
If you don't have permissions to check out, you'll need to let your repository maintainer know so they can set up an account for you.
On Sourceforge or another cloud service, you'll need to make your own account and then ask to be added to the developer group for the project.

Now you have the code!
But when you try to open the Visual Studio solution nothing works.
You need to regenerate the project files for your machine.
Unreal Engine makes the really easy, you just need to right click on the uproject file and select "Generate Visual Studio project files."

From here you should be able to edit files and make all of your contributions.

I'll edit this soon to add how you can safely add the source control to work inside the editor so you don't have to do all of your revision control by hand.

