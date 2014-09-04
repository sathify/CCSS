component-css
=============

Large web applications generally have a lot of CSS files and many developers working on them simultaneously. With the advent of so many frameworks, guidelines, tools and methodologies like OOCSS, SMACSS, BEM, etc., developers need a CSS architecture that is maintainable, manageable, and scalable.

As a frontend engineer, I believe that component-based web development is the way forward. [Web components](http://css-tricks.com/modular-future-web-components/)  are a collection of standards that are working their way through the W3C.  They allow us to bundle up markup and styles into reusable HTML elements which are *truly encapsulated*. What this means is we need to start thinking about **component based CSS development**. While the browser makers are implementing these standards, we can use *soft-encapsulation* in the meantime.

Component CSS is an architecture which simplifies the CSS authoring experience for large web applications.


1. [Elements](#elements)
2. [Principles](#principles)
3. [Directory Structure](#directory)
4. [Naming Conventions for Simplified BEM ](#naming)
5. [Architecture & Design](#architecture)
6. [Example](#example)


<a name="elements"></a>
## Elements of Component CSS

Below are the major elements used either fully or in a modified way to achieve the best configuration for the component-css architecture.


##### SMACSS
SMACSS stands for Scalable and Modular Architecture for CSS. It is more of a style guide than a rigid framework. Read about [SMACSS](http://smacss.com) for background on the structure as component css uses it.


##### BEM
BEM stands for “Block”, “Element”, “Modifier”. It is a front-end methodology which is a new way of thinking when developing web interfaces. The guys at Yandex came up with BEM and more information can be found  [here](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/).

##### SASS
SASS is CSS with [superpowers](http://davidwalsh.name/future-sass). Highly recommend it but you can also use LESS if you prefer that. Please refer to the [SASS documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html) for more information.


##### Compass
  Compass has no class definitions, it is an extension of SASS which provides a lot of utilities. It is used for general useful mixins, and sass compilation.
  Compass mixins should nearly *always* be used in cases where vendor prefixes are required.


<a name="principles"></a>
## Principles of Component CSS

##### Component-based
Write small and independent components which are reusable. A reusable css component is one which does not only exist on a specific part of the DOM tree or require the use of certain element types. If necessary, extra HTML elements should be used to make a component reusable.

##### Modular and Isolated
Components should have everything necessary to a certain part of the UI and have a single focus. It should also be isolated, meaning it should not directly modify or depend on another component.

Isolation is more important that code reuse across components as it can increase dependencies and tight coupling, eventually making the CSS less manageable.

##### Composable
When authoring CSS in a way that aims to reduce the amount of time spent writing it, one should think of it in a way to spend more time changing HTML classes on elements for modifying or adding styles. It is much easier for all developers to author css when it is like assembling lego blocks than to fight the CSS war. CSS classes are the building blocks which should be used to compose styles.

##### Documentation
Most people assume CSS is self-explanatory. In fact, this is usually not the case! CSS components must be documented clearly which describes how they should be used and what it does.

<a name="directory"></a>
## Directory Structure
Below is the directory structure, I have also included an example set up in this repo.
<code><pre>styles
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
    └── **scss
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
            └── _light.scss**</pre></code>

Only edit/author the files in the <code>scss/</code> folder denoted in the bold above. This allows for updating external libraries easily which are in the `ext/`. Many applications start out with an external CSS framework like bootstrap or foundation, etc. so I added them in the example set up in the `ext/` folder. It's absolutely fine to have all the CSS written from scratch and everything else mentioned above applies. 

The directory `components/` has desired efficacy in an AngularJS application but please feel free to customize it. More information is in [Architecture](#architecture) section.

In the HTML page, include all the <code>.css</code> files from <code>style/</code> folder which are generated after the SCSS compiles using grunt, compass, etc. Never alter them.

<a name="naming"></a>
## Naming Conventions for Simplified BEM
 - `u-className` Global base/utility classes
 - `img-className` Global image classes
 - `animate-className` Global animation classes
 - `ComponentName` Standard Components (B)
 - `ComponentName-elementName` Conponent's Element (E)
 - `ComponentName--modifierName` Component's Modifier (M)

Note the UpperCamelCase Component name to indicate that it is the master element and denotes the boundary of the component. Whereas the element and modifier names are elementName and modifierName respectively. Do not use <code>-</code> to separate out component names as it signifies the start of an element/element name.


<a name="architecture"></a>
## Architecture and Design

##### Grunt
Grunt is a great task runner that can automate most of the tasks. Highly recommend using it to configure and compile the CSS. There are also other task runners but in general use it to compile all the necessary SCSS files into CSS, to watch for changes and recompile when changes are detected.

##### File organization
Please take a look the the directory structure which is derived from smacss. Notice the <code>ext/</code> where all the external frameworks like bootstrap reside. Anything under <code>ext/</code> should not be overridden as it makes it easier to upgrade and maintain the external CSS frameworks. If you want to override please refer to <code>base/</code> folder for framework overrides file or add it.

<code>base/</code> is where global base styles used application wide exits.

<code>_base.scss</code> Base styles for element selectors only. These are sort of "CSS resets"

<code>_base-classes.scss</code> These are all utility classes used application wide across many pages, views, and components. Prefix class names with <code>u-</code>

<code>images.scss</code> Use this as a SCSS compilation source. It should define and inline all site images as Data URIs. <code>/app/styles/images.css</code> is generated from this file.

<code>_animate.scss</code> All animation classes used application wide.

<code>_bootstrap-overrides.scss</code> Framework overrides only. Sometimes the level of specificity of framework selectors is so high that overriding them requires long specific selectors. Overriding at a global level should not be done in the context of a SCSS component, instead all global overrides go here.

##### Components
Any unit of reusable CSS not mentioned above is considered a "component". We use AngularJS so I categorized them to 3 types of CSS components: view/page, directive, and standard; and hence the directory structure which is derived from SMACSS. In the example setup in the [github repository](https://github.com/sathify/component-css/tree/master/styles), I created explicit folders to be clear. If your application is small, you may put them in one folder. All components follow the [modified BEM naming convention](https://github.com/sathify/component-css#naming) in combination with the CamelCase. This got me *great wins* in encouraging other team members to follow BEM style syntax. It also avoided a lot of confusion when moving away from using the typical BEM style with <code>-, --, & __</code> symbols which generate class names like <code>module-name__child-name--modifier-name</code>!


Another important thing would be to make sure CSS class definition order in a component reflects the html view. This makes it easier to scan, style, edit and apply classes easily. Finally, it's a good idea to have an extensive style-guide for the web application and follow guidelines for [CSS](https://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) and SASS (avoid <code>@extends</code>).

<a name="example"></a>
## Example

Refer to the [code](https://github.com/sathify/component-css/tree/master/styles) for an example set-up of the CSS.

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

Refer to the simplified [BEM mixin](https://github.com/sathify/component-css/blob/master/styles/scss/mixins/_bem.scss) which uses reference selector to achieve this and is simpler than @at-root. [Working with BEM](http://www.integralist.co.uk/posts/maintainable-css-with-bem/) got way easier in version Sass 3.3> which gives us the ability to write maintainable code that is easy to understand.

### Credits and Reading

* [SMACSS](https://smacss.com/)
* [SASS Features](http://davidwalsh.name/future-sass)
* [BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)
* [Component Based Development](http://en.wikipedia.org/wiki/Component-based_software_engineering)
* [Composabile Design](http://en.wikipedia.org/wiki/Composability)
* [Web Components](http://css-tricks.com/modular-future-web-components/)
* [CSS guidlines](https://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) 
* [CSS Tips](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
* [Debug CSS](https://github.com/yahoo/debugCSS)
* [High-level Guidelines](http://cssguidelin.es/)
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [Wikipedia definition of composability](http://en.wikipedia.org/wiki/Composability)
