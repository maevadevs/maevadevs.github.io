---
layout: post
title: How To Manage Multiple Node Versions Efficently
category: NodeJS
tags: [nodejs, nvm]
---

When you work with NodeJS projects, you will realize that you need multiple versions of NodeJS and NPM (and their respective Global modules) to run and test different projects, maybe least two(2) major versions. I propose the following solution to deal with this issue.

---

Note that this is not the only solution but this is a way I found that works best in maintaining the NodeJS versions that I require in a logical and streamlined manner, in my humble opinion.

Of course, others people might have a different ways and solutions and that is totally okay. As developers, we know that there are many ways to solve one problem. But if you are interested about my way, I invite you to keep reading.

## Steps

- [1. Remove `system` Node](#01)
  - [For MacOS: Remove `system` Node using `brew`](#01-01)
- [Install `nvm`](#02)
  - [For MacOS: Install `nvm` using `brew`](#02-01)
  - [For MacOS: Change `.bash_profile`](#02-01-01)
- [Installing and Maintaining Node Versions with `nvm`](#03)

## 1. Remove `system` Node (Optional)

<a name="01"></a>

Before you use this method, make sure that you do not have a system-installed Node on your machine. System-installed Node often creates some confusion and bugs with the NVM-installed versions.

### For MacOS: Remove `system` Node using `brew`

<a name="01-01"></a>

If you have Node with brew, uninstall the `system` node. Note: This will also remove your global packages so make sure to take a not of them.

{% highlight sh %}
brew uninstall node
brew update && brew upgrade
brew cleanup
{% endhighlight %}

*Note: To review if there are any conflicting packages of brew, `brew doctor` is always helpful.*

## 2. Install `nvm`

<a name="02"></a>

NVM is the Node Version Manager. It allows to maintain multiple versions of node/npm and switch back and forth between those versions as projects requires.

### For MacOS: Install `nvm` using `brew`

<a name="02-01"></a>

To install NVM, run the following:

{% highlight sh %}
brew update && brew upgrade
brew install nvm
brew postinstall nvm
brew cleanup
{% endhighlight %}

*Note: Follow the same steps as above for system node to upgrade or uninstall nvm.*

#### For MacOS: Change `.bash_profile`

<a name="02-01-01"></a>

To make sure that the command line finds the `nvm` command, add these lines to the `.bash_profile`:

{% highlight sh %}
# Load nvm
export NVM_DIR="/Users/[yourusername]/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm`
{% endhighlight %}

Then, reload the `.bash_profile` source from the terminal:

{% highlight sh %}
source ~/.bash_profile`
{% endhighlight %}

Verify that the system nvm works correctly:

{% highlight sh %}
which nvm
nvm --version
{% endhighlight %}

### 3. Installing and Maintaining Node Versions with `nvm`

<a name="03"></a>

Now that NVM is installed, we can install multiple versions of Node. To check for the available versions to install:

{% highlight sh %}
nvm ls-remote
{% endhighlight %}

To install versions of node (e.g. v7.4.0 and v6.9.4):

{% highlight sh %}
nvm install 7.4.0
nvm install 6.9.4
{% endhighlight %}

To check which versions are currently installed on our system (The currently used is pointed by an arrow):

{% highlight sh %}
nvm ls
{% endhighlight %}

To swith to a different installed version (e.g. from v7.4.0 to v6.9.4)

{% highlight sh %}
nvm use 6.9.4
{% endhighlight %}

To verify which node/npm is currently being use, we can simply check them again.

{% highlight sh %}
which npm
npm --version
which node
node --version
{% endhighlight %}

To upgrade to a new version and move the global modules to the new version: (e.g. from v6.8.0 to v6.9.4)

{% highlight sh %}
nvm install 6.9.4 --reinstall-packages-from=6.8.0
nvm uninstall 6.8.0
{% endhighlight %}

Here is an example of my quick automation shortcut for a streamlined upgrade

{% highlight sh %}
nvm install 6.9.4 --reinstall-packages-from=6.8.0 && nvm uninstall 6.8.0 && nvm use 6
{% endhighlight %}

And finally, to uninstall a version altogether, without upgrading

{% highlight sh %}
nvm uninstall 6.8.0
{% endhighlight %}
