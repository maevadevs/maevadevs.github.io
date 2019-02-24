---
layout: post
title: Setup ESLint In VSCode With `create-react-app` Without Ejecting
---

In this post, I explain how I got to setup ESLint with `create-react-app` (CRA) in Visual Studio Code, *without ejecting!* 

Typically, we are asked to eject our CRA application when wanting to get advantage of ESLint integration with VS Code. However, here are some very easy steps I used for an easy fix while:

- Making code linting work in VSCode, AND
- Not breaking CRA setup (no eject)

## Steps

1. Make sure you have installed the [`ESLint` plugin for VS Code by Dirk Baeumer](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint). However, **DO NOT install the npm `eslint`, whether locally or globally!** The installation of the plugins says you should npm install `eslint` but since CRA already provides its own, we skip that altogether.

1. Make sure you configure your [VSCode User and Workspace Settings](https://code.visualstudio.com/docs/getstarted/settings) with the settings you like for your ESLint User Config in the VS Code settings. I personally like to have `Auto Fix On Save` switched on, but you can personalize as you like.

1. Add your `.eslintrc.json` to the project root, or run `npx eslint --init` to create one. If you create one manually, then jump to step 5 from here. (Note: We use `npx` here so that we simply execute `--init` without installing the `eslint` dependency. See step 1: Not installing `eslint`)

1. The `npx` command will create the `eslintrc` file then will crash without installing the depedencies because it cannot find `eslint.` That is fine. Carry on.

1. The previous command, or your manually-created `eslintrc`, might have other dependencies other than `eslint`. You need to install any required additional dependencies if they were not already done. The example below shows the case for the React plugin.

```shell
yarn add -D eslint-plugin-react
```

6. Finally, make sure to have `"plugin:react/recommended"` setup in `.eslintrc.json`. Replace `extends` with an array if needed. The order here might be important to make the correct linting work.

```json
"extends": [
  "eslint:recommended",
  "plugin:react/recommended"
]
```

That's it! Now, refresh your files or re-open your project folder if needed and checkout those squigly ESLint familiar underline. And if you switched on `Auto Fix On Save` in your VS Code  User Settings, then CTRL+S or CMD+S will do all apply all the fixes for you.

Happy coding!
