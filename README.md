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


<a name="naming"></a>
### Naming Conventions for Simplified BEM
 - `u-className` Global base/utility classes
 - `img-className` Global image classes
 - `animate-className` Animation classes
 - `ComponentName` Standard Modules (B)
 - `ComponentName-elementName` Standard Modules Element (E)
 - `ComponentName--modifierName` Standard Modules Modifier (M)
 
Please note the UpperCamelCase Component name to indicate that it is the master element and is the boundary of the component. Whereas the element and modifier names are elementName and modifierName respectively. Please do not use <code>-</code> to separate out component names as it signifies the start of an element/element name.
