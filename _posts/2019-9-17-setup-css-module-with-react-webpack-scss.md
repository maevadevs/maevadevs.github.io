---
layout: post
title: Setup CSS Module With React, Webpack, and SCSS
category: React
tags: [scss, css, react, webpack]
---

As we often compare Angular with React, one of the thing that I like about Angular is the style encapsulation that we assign to components. It makes the styles only applied to the local elements of the component and does not become global, even though the final bundle is still a single compiled `styles.css` file. Here is how we can achieve that with React.

---

## Setup With CRA

If you are using CRA 2.0+, all you need to do is to name the local style file to `[ComponentName].module.css`. This convention is recognized by create-react-app as a modular css.

## Manual Setup

On the over hand, here is the setup if not using CRA. Assuming that you have set up your React app using Babel and Webpack, we just need to cusomtize `css-loader` for this setup. CSS Module is already supported by Babel's `css-loader`. We just need to hook it up with `sass-loader` in `webpack.config.js`.

{% highlight js %}
const CSSExtract = new MiniCssExtractPlugin() // Default output bundle filename: main.css

const scssLoader = {
  test: /\.s?css$/,
  use: [{
    loader: MiniCssExtractPlugin.loader,
    options: {
      sourceMap: true // Mapping to original scss source
    }
  }, {
    loader: 'css-loader',
    options: {
      sourceMap: true, // Mapping to original scss source
      modules: {
        mode: 'local', // Enable local component styles scoping
        localIdentName: '[local]--[hash:base64:7]' // [local] is placeholder for the CSS selector: e.g. container--b4ku7nb
      }
    }
  }, {
    loader: 'sass-loader',
    options: {
      sourceMap: true // Mapping to original scss source
    }
  }]
}

module.exports = {
  mode: 'production',
  //... Other setup lines here
  module: {
    rules: [
      babelLoader,
      scssLoader,
      fileLoader
    ]
  },
  plugins: [
    CSSExtract
  ]
}
{% endhighlight %}

There are multiple options that can be used to configure CSS Module with `css-loader`. [Check the documentation](https://github.com/webpack-contrib/css-loader#modules) for more info.

## How it works

Now, here is the folder structure of components. Let's look at a custom `TextInput` component as an example.

{% highlight js %}
TextInput/
|- index.js
|- styles.scss
|- TextInput.test.js
{% endhighlight %}

`styles.scss` can contain the styles specific for this component. Also, keep in mind that *all css rules are valid scss rules.* So using a SCSS setup is much flexible than simpy using CSS.

{% highlight scss %}
/* --- styles.scss --- */
// SCSS Variables
$fontSize: 16;
$fontWeight: 100;
$fontFamily: Arial, Helvetica, sans-serif;

// Element Styles
.container {
  flex: 1;
  flex-direction: 'row';
  align-items: 'center';
}
.label {
  font-family: $fontFamily;
  font-size: $fontSize;
  font-weight: $fontWeight;
  padding-left: 20;
  flex: 1;
}
.input {
  color: '#000';
  padding-right: 5;
  padding-left: 5;
  font-size: $fontSize;
  flex: 3;
}
{% endhighlight %}

Now, `styles.scss` can be imported directly into `index.js` as any other ES6 modules and styles can be applied as if they were props off that object. It is also possible to apply destructuring here but be careful not to have variable collision. (e.g. `label` vs `styles.label`)

{% highlight jsx %}
/* --- index.js --- */

import { container }, styles from './styles.scss'

class TextInput extends Component {
  render() {
    const { type, label, placeholder } = this.props
    return (
      <div className={container}>
        {
          label &&
          <label htmlFor='text-input' className={styles.label}>
            {label}
          </label>
        }
        <input
          type={type}
          placeholder={placeholder}
          ref={this.textInputRef}
          name='text-input'
          className={styles.input}
          value={this.state.value}
          onChange={e => this.handleChangeValueLocal(this.textInputRef.current.value)}
        />
      </div>
    )
  }
}
{% endhighlight %}
