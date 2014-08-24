component-css
=============

CSS architecture for the future web 

Generally large web applications have lot of css files with many developers working on them simultaneously. With the advent of so many frameworks, guidelines, tools and methodologies like SMASS, BEM, OOCSS, etc. there needs to be a css architecture which defines a way to author CSS which is maintainable, manageable, and scalable. 

We all know reusable, component-based web development is definitely the way forward. [Web components](http://css-tricks.com/modular-future-web-components/)  which are a collection of standards are working their way through the W3C.  They allows us to bundle up markup and styles in to reusable HTML elements which are truly encapsulated. What this means is we need to start thinking component based css development. While browsers are coming up with implementing web components standards, the current phase of developing large web applications with many css components is in a transition and could follow soft-encapsulation.

Component CSS aims to improve the CSS authoring experience for large web applications with component-based development mind set at the core. 


1. [Elements](#elements)
2. [Principles](#principles)
3. [Architecture & Design](#architecture)
4. [Directory Structure](#directory)
5. [Naming Conventions for Simplified BEM ](#naming)
6. [Examples](#examples)



<a name="elements"></a>
## Elements of Component CSS 

Below are the major elements used either fully or in a modified way to achieve the best configuration for the component-css architecture. 


##### SMACSS
SMACSS stands for Scalable and Modular Architecture for CSS. It is more of a style guide than a rigid framework to design and author scalable css for big applications. Read about [SMACSS](http://smacss.com) for background on the structure as component css uses it. 
 

##### BEM
BEM stands for “Block”, “Element”, “Modifier”. It is a front-end methodology which is a new way of thinking when developing web interfaces. The guys at Yandex came up with BEM and more information is  [here](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

##### SASS
SASS is great and refer to the [SASS documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html).


##### Compass
  Compass has no class definitions, only mixins. It is used for general useful mixins, and sass compilation.
  Compass mixins should nearly *always* be used in cases where vendor prefixes are required.


<a name="principles"></a>
## Principles of Component CSS  

##### Component-based
Write small and independent components which are reusable. A flexible and reusable css component is one which does not only exist on a specific part of DOM tree or require the use of certain element types. If necessary extra html elements should be used to make a component reusable and flexible. 

##### Modular and Isolated
Components should have everything necessary to a certain part of the UI and have a single focus. It should also be isolated, meaning it should not directly modify another component.  

Isolation is more important that trying to reuse too much code across components as it can increase dependences and tight coupling. Eventually making the CSS less manageable. 

##### Composable
Definition from [wikipedia](http://en.wikipedia.org/wiki/Composability)- A highly composable system provides recombinant components that can be selected and assembled in various combinations to satisfy specific user requirements. 

When authoring CSS in a way that aims to reduce the amount of time spent on writing and editing CSS, one should think of it in a way to spend more time changing HTML classes on elements for modifying or adding styles. It is much easier for all developers to author css when it is similar to assembling lego blocks than to fight the CSS war. CSS classes are the building blocks which is used to compose styles. 

##### Documentation
Most people assume CSS is self-explanatory which is not the case most times. CSS components must be documented clearly which describes how they should be used and what it does. 


<a name="naming"></a>
## Naming Conventions for Simplified BEM
 - `u-className` Global base/utility classes
 - `img-className` Global image classes
 - `animate-className` Animation classes
 - `ComponentName` Standard Modules (B)
 - `ComponentName-elementName` Standard Modules Element (E)
 - `ComponentName--modifierName` Standard Modules Modifier (M)
 
Please note the UpperCamelCase Component name to indicate that it is the master element and is the boundary of the component. Whereas the element and modifier names are elementName and modifierName respectively. Please do not use <code>-</code> to separate out component names as it signifies the start of an element/element name.


<a name="naming"></a>
## Architecture and Design

##### Grunt 
Grunt is a great task runner that can automate all the tasks. Highly recommend using it to configure and compile the CSS. There are also other task runners but in general use it to compile all the necessary SCSS files into CSS, to watch for changes and recompile when changes are detected. 

##### File organization
Please take a look the the directory structure which is derived from smacss. Notice the <code>ext/</code> where all the external frameworks like bootstrap reside. Anything under <code>ext/</code> should not be overridden as it makes it easier to upgrade and maintain the external CSS frameworks. If you want to override please refer to <code>base/</code> folder for framework overrides file or add it. 

<code>base/</code> is where global base styles used application wide exits.
     
<code>_base.scss</code> Base styles for element selectors only. These are sort of "CSS resets" 

<code>_base-classes.scss</code> These are all utility classes used application wide across many pages, views, and components. Prefix class names with <code>u-</code>

<code>_images.scss</code> Please use this as a SCSS compilation source. It should define and inline all site images at Data URIs. <code>/app/styles/images.css</code> is generated from this file.

<code>_animate.scss</code> All animation classes used application wide. 

<code>_bootstrap-overrides.scss</code> Framework overrides only. Sometimes the level of specificity of framework selectors is so high that overriding them requires long specific selectors. Overriding at a global level should NOT be done in context of an SCSS view, module, etc, instead all global overrides go here.


##### Components
Any unit of reusable CSS not mentioned above is considered a "component". We use AngularJS so I categorized them to 3 types of CSS components: view, directive, and standard; and hence the directory structure which is derived from SMACSS. All components follow the above mentioned modified BEM naming convention in combination with the CamelCase. This got me *great wins* in making other team members start following BEM style syntax and also avoided lots of confusion when not using the following <code>-, --, & __</code>!


Finally, please have an extensive style-guide for the web application and follow guidelines for [CSS](https://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) and SASS (avoid <code>@extends</code>).
