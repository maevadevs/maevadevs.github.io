---
layout: post
title: Setup ESLint In VSCode With `create-react-app` Without Ejecting
---

In this post, I explain how I got to setup ESLint with `create-react-app` (CRA) in Visual Studio Code, *without ejecting!*

---

Typically, we are asked to eject our CRA application when wanting to get advantage of ESLint integration with VS Code. However, here are some very easy steps I used for an easy fix while:

- Making code linting work in VSCode, AND
- Not breaking CRA setup (no eject)

## Steps

1. Make sure you have installed the [`ESLint` plugin for VS Code by Dirk Baeumer](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint). However, **DO NOT install the npm `eslint`, whether locally or globally!** The installation of the plugins says you should npm install `eslint` but since CRA already provides its own, we skip that altogether.

1. Make sure you configure your [VSCode User and Workspace Settings](https://code.visualstudio.com/docs/getstarted/settings) with the settings you like for your ESLint User Config in the VS Code settings. I personally like to have `Auto Fix On Save` switched on, but you can personalize as you like.

1. Add your `.eslintrc.json` to the project root, or run `npx eslint --init` to create one. If you create one manually, then jump to step 5 from here. (Note: We use `npx` here so that we simply execute `--init` without installing the `eslint` dependency. See step 1: Not installing `eslint`)

1. The `npx` command will create the `eslintrc` file. If it asks *Would you like to install them now with npm?*, make sure to reply `n`. We want to make sure we do not install `eslint`. However, go ahead an install all other dependencies other than `eslint`. You need to install any required additional dependencies if they were not already done. The example below shows the case for the React plugin, needed to support React linting.

{% highlight sh %}
yarn add -D eslint-plugin-react
{% endhighlight %}

5. Finally, make sure to have `"plugin:react/recommended"` setup in `eslintrc`. Replace `extends` with an array if needed. The order here is important to make the correct linting work.

{% highlight json %}
"extends": [
  "eslint:recommended",
  "plugin:react/recommended"
]
{% endhighlight %}

Here is a full rules list example that I use on my project.

{% highlight json %}
{
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended"
  ],
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 2018,
    "sourceType": "module"
  },
  "plugins": ["react"],
  "rules": {
    "indent": ["error", 2],
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "single"],
    "semi": ["error", "always"]
  }
}
{% endhighlight %}

That's it! Now, refresh your files or re-open your project folder if needed and checkout those squigly ESLint familiar underline. And if you switched on `Auto Fix On Save` in your VS Code  User Settings, then CTRL+S or CMD+S will do all apply all the fixes for you.

## Summary

Basically, as long as you don't npm install `eslint` itself, you are good. The conflict only happens when you npm install `eslint` because CRA already has a specific version that it needs.

Happy coding!

## Versions Used

- Node: `10.15.1`
- Yarn: `1.13.0`
- NPM: `6.8.0`
- create-react-app: Always `latest` when using `npx`
