component-css
=============

CSS architecture for the future web 


1. [Elements of Component CSS](#elements)
2. [Principles of Component CSS](#principles)
3. [Architecture & Design](#architecture)
4. [Directory Structure Organization](#directory)
5. [Naming Conventions for Modified BEM ](#naming)
6. [Examples](#examples)


<a name="naming"></a>
### Naming Conventions for Modified BEM
 - `u-className` Global base/utility classes
 - `img-className` Global image classes
 - `animate-className` Animation classes
 - `ComponentName` Standard Modules (B)
 - `ComponentName-elementName` Standard Modules Element (E)
 - `ComponentName--modifierName` Standard Modules Modifier (M)
 
Please note the UpperCamelCase Component name to indicate that it is the master element and is the boundary of the component. Whereas the element and modifier names are elementName and modifierName respectively. Please do not use <code>-</code> to separate out component names as it signifies the start of an element/element name.
