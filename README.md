CCSS
====

CCSS [Component CSS] is an architecture which simplifies the CSS authoring experience for large web applications.

##### Why?
Large web applications generally have a lot of CSS files and many developers working on them simultaneously. With the advent of so many frameworks, guidelines, tools and methodologies (OOCSS, SMACSS, BEM, ...), developers need a CSS architecture that is maintainable, manageable, and scalable.

As a frontend engineer, I believe that component-based web development is the way forward. [Web components](http://css-tricks.com/modular-future-web-components/) are a collection of standards that are working their way through the W3C. They allow us to bundle up markup and styles into reusable HTML elements which are *truly encapsulated*. What this means is we need to start thinking about **component based CSS development**. While the browser makers are implementing these standards, we can use *soft-encapsulation* in the meantime.

##### When?
As a developer, use it when you are setting up the CSS architecture for a complex web application.


## Contents

1. [Elements](#elements)
2. [Principles](#principles)
3. [Directory Structure](#directory)
4. [Naming Conventions - Simplified BEM ](#naming)
5. [Architecture & Design](#architecture)
6. [Example](#example)
7. [Contributing](#contributing)
8. [Resources](#resources)


<a id="elements"></a>
## Elements of CCSS

Below are the major elements used either fully or in a modified way to achieve the best configuration for the CCSS architecture.


##### SMACSS
SMACSS stands for Scalable and Modular Architecture for CSS. It is more of a style guide than a rigid framework. Read about [SMACSS](http://smacss.com) for background on the structure as CCSS uses it.


##### BEM
BEM stands for “Block”, “Element”, “Modifier”. It is a front-end methodology which is a new way of thinking when developing web interfaces. The guys at Yandex came up with BEM and more information can be found [here](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/).

##### SASS
SASS is CSS with [superpowers](http://davidwalsh.name/future-sass). Highly recommend it but you can also use LESS if you prefer that. Please refer to the [SASS documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html) for more information.


##### Compass
Compass has no class definitions, it is an extension of SASS which provides a lot of utilities. It is used for general useful mixins, and sass compilation. Compass mixins should nearly *always* be used in cases where vendor prefixes are required. This again is a nice to have and [Bourbon](http://bourbon.io/), on the first look is a great alternative. 


<a id="principles"></a>
## Principles of CCSS

##### Component-based
Write small and independent components which are reusable. A reusable css component is one which does not only exist on a specific part of the DOM tree or require the use of certain element types. If necessary, extra HTML elements should be used to make a component reusable.

##### Modular and Isolated
Components should have everything necessary to a certain part of the UI and have a single focus. It should also be isolated, meaning it should not directly modify or depend on another component.

Isolation is more important than code reuse across components as it can increase dependencies and tight coupling, eventually making the CSS less manageable.

##### Composable
When authoring CSS in a way that aims to reduce the amount of time spent writing it, one should think of it in a way to spend more time changing HTML classes on elements for modifying or adding styles. It is much easier for all developers to author CSS when it is like assembling lego blocks than to fight the [CSS war](https://s3.amazonaws.com/zeroviscosity/d3-js-step-by-step/step-3-adding-a-legend/css.gif). CSS classes are the building blocks which should be used to compose styles.

##### Predictable
Predictable means when you author CSS, your rules behave as you expect. This is important for large applications which have many pages. Avoid using overly complicated selectors and generic class names, as these can lead to unpredictable CSS.

##### Documentation
Most people assume CSS is self-explanatory. In fact, this is usually not the case! CSS components must have clear documentation which describe what they do and how they should be used.

<a id="directory"></a>
## Directory Structure
Below is an example directory structure for easier visualization, I have also included an example setup in this repo.
<pre><code>styles
    ├── bootstrap.css
    ├── ext
    │   ├── bootstrap
    │   │   ├── _settings.scss
    │   │   └── bootstrap.scss
    │   └── font-awesome
    │       └── font-awesome.scss
    ├── font-awesome.css
    ├── images.css
    ├── main.css
    └── scss
        ├── _config.scss
        ├── base
        │   ├── _animation-classes.scss
        │   ├── _base-classes.scss
        │   ├── _base.scss
        │   └── images.scss
        ├── components
        │   ├── directives
        │   │   ├── _empty-state.scss
        │   │   ├── _legend.scss
        │   │   └── _status-message.scss
        │   ├── pages
        │   │   ├── _404.scss
        │   │   └── _redirect.scss
        │   └── standard
        │       ├── _alarm-state.scss
        │       ├── _graph-message.scss
        │       └── _panel.scss
        ├── main.scss
        ├── mixins
        │   ├── _animation.scss
        │   ├── _bem.scss
        │   └── _icon.scss
        └── themes
            └── _light.scss</code></pre>

Only edit/author the files in the `scss/` folder. This allows for updating external libraries easily which are in the `ext/`. Many applications start out with an external CSS framework like Bootstrap or Foundation, so I added them in the example setup in the `ext/` folder. It's absolutely fine to have all the CSS written from scratch; everything else mentioned above still applies.

The example `components/` directory is well-suited for an AngularJS application, but can be customized for other frameworks or applications. More information is in the [Architecture](#architecture) section.

In the HTML page, include all the `.css` files from the `style/` folder, which contains all the compiled CSS (from Grunt, Compass, etc.). Never alter them.

<a id="naming"></a>
## Naming Conventions - Simplified BEM

 - `u-className` Global base/utility classes
 - `img-className` Global image classes
 - `animate-className` Global animation classes
 - `ComponentName` Standard Components (B)
 - `ComponentName-elementName` Component's Element (E)
 - `ComponentName--modifierName` Component's Modifier (M)

Note the UpperCamelCase Component name to indicate that it is the master element; this denotes that it is the *boundary of the component*. Element and modifier names are elementName and modifierName, respectively. Do not use `-` to separate out component names, as these signify the start of an element/element name.


<a id="architecture"></a>
## Architecture and Design

##### Grunt
Grunt is a great task runner that can automate many common chores (such as compiling CSS or validating HTML). There are also other task runners; an ideal workflow involves using one to watch files under development and recompile the CSS when changes are made.

##### File organization
Please take a look at the directory structure which is derived from SMACSS. Notice the `ext/` directory, which contains all external frameworks (like Bootstrap). To keep upgrading easy, these should not be modified; instead, overrides and extensions should be placed in the `base/` directory.

`base/` is where global base styles used application wide exists.

`_base.scss` Base styles for element selectors only. These are sort of "CSS resets".

`_base-classes.scss` These are all utility classes used application wide across many pages, views, and components. Prefix class names with `u-`

`images.scss` Use this as a SCSS compilation source. It should define and inline all site images as Data URIs. `/app/styles/images.css` is generated from this file.

`_animate.scss` All application-wide animation classes.

`_bootstrap-overrides.scss` Framework overrides only. Sometimes the level of specificity of framework selectors is so high that overriding them requires long specific selectors. Overriding at a global level should not be done in the context of a SCSS component, instead all global overrides go here.

##### Components
Any unit of reusable CSS not mentioned above is considered a "component". We use AngularJS so I categorized them to 3 types of CSS components: view/page, directive, and standard; and hence the directory structure which is derived from SMACSS. In the example setup in the [GitHub repository](https://github.com/sathify/ccss/tree/master/styles), I created explicit folders to be clear. If your application is small, you may put them in one folder. All components follow the [modified BEM naming convention](https://github.com/sathify/ccss#naming) in combination with the CamelCase. This got me *great wins* in encouraging other team members to follow BEM style syntax. It also avoided a lot of confusion when moving away from using the typical BEM style with the `-`, `--`, and `__` symbols which generate class names like `module-name__child-name--modifier-name`!

It is also important that the CSS class definition order in a component reflects the html view. This makes it easier to scan, style, edit and apply classes easily. Finally, it's a good idea to have an extensive style-guide for the web application and follow guidelines for [CSS](https://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) and SASS (avoid `@extends`).

<a id="example"></a>
## Example

Refer to the [code](https://github.com/sathify/ccss/tree/master/styles) for an example setup of the CSS.

Here is an example component in SASS.
```
.ProductRating {
  // nested element
  @include e(title) {
    ...
  }
  // nested element
  @include e(star) {
    ...
    // nested element's modifier
    @include m(active) {
      ...
    }
  }
}
```

It compiles to the following CSS:

```
.ProductRating {
  ...
}
// nested element
.ProductRating-title {
  ...
}
// nested element
.ProductRating-star {
  ...
}
// nested element's modifier
.ProductRating-star--active {
  ...
}
```

Your HTML might look something like below.

    <div class="ProductRating">
      <img alt="Company logo" class="img-logo">
      <h3 class="ProductRating-title">Title</h3>
      <div class="u-starHolder">
        <span class="ProductRating-star ProductRating-star--active"></span>
        <span class="ProductRating-star ProductRating-star--active"></span>
        <span class="ProductRating-star ProductRating-star--active"></span>
        <span class="ProductRating-star"></span>
      </div>
    </div>

Refer to the simplified [BEM mixin](https://github.com/sathify/ccss/blob/master/styles/scss/mixins/_bem.scss) which uses reference selector to achieve this and is simpler than `@at-root`. [Working with BEM](http://www.integralist.co.uk/posts/maintainable-css-with-bem/) became much easier in version Sass 3.3+, which gives us the ability to write maintainable code that is easy to understand.

<a id="contributing"></a>
## Contributing

Contributions in the form of issues/PRs for adding more examples, improvements with post processing, clarifications, etc. are most helpful.

Thanks for the initial contributions from [@jonrahoi](https://github.com/jonrahoi) [@ksheedlo](https://github.com/ksheedlo) [@leemunroe](https://github.com/leemunroe) and [@eddywashere](https://github.com/eddywashere).

<a id="resources"></a>
## Resources and Credits

##### CSS
* [SMACSS](https://smacss.com/)
* [SASS Features](http://davidwalsh.name/future-sass)
* [BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)
* [CSS guidelines](https://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)
* [CSS Tips](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
* [Debug CSS](https://github.com/yahoo/debugCSS)
* [High-level Guidelines](http://cssguidelin.es/)
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [Single Responsibility](http://drewbarontini.com/articles/single-responsibility/)

##### General
* [Web Components](http://css-tricks.com/modular-future-web-components/)
* [Component Based Development](http://en.wikipedia.org/wiki/Component-based_software_engineering)
* [Wikipedia definition of composability](http://en.wikipedia.org/wiki/Composability)

##### Credits
* [Nicholas Gallager](http://nicolasgallagher.com/)
* [Thierry Koblentz](https://twitter.com/thierrykoblentz)
* [Harry Roberts](http://csswizardry.com/work/)
