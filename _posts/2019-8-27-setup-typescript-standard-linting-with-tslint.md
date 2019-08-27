---
layout: post
title: Setup TypeScript Standard Linting With TSLint
category: TypeScript
tags: [typescript, tslint, eslint]
---

For small TypeScript-based project, here is the setup to get easy linting with TypeScript using TS *Standard* Style (though this can also be used for any other TS Style)

---

This is a very easy setup that can be done in 3 steps. I am using VS Code and `yarn` in this example.

- Install the `TSLint` editor plugin for your Text Editor
- Add to devDependencies to project: `yarn add -D tslint tslint-config-standard`
- Add `tslint.json` to project root with the following content:

{% highlight json %}
{
  "defaultSeverity": "error",
  "extends": ["tslint-config-standard"],
  "jsRules": {},
  "rules": {},
  "rulesDirectory": []
}
{% endhighlight %}

*Note:* If you don't like the *Standard* style, you can simply replace the rules to extend from with something else, or define your own `rules`
