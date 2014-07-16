#Spot CSS Framework
> A modern day CSS framework that follows a flexible approach to creating
scalable stylesheets.

##Introduction
Cascading stylsheets were built to be used on sites that are very different
from the web applications that we're currently building. This dictates the
need to abandon the traditional way of styling webpages, and implement a
framework that mirrors the way applications are programatically architected.
That is, we should borrow from other web domains, and apply those best
practices to web design: modularity, a separation of concerns, DRY,
encapsulation, convention, etc.

###Difficulties
On smaller/short-lived projects, it's often okay to not worry about scalablity
and how the current approach will impact future design and development.
However, on web applications that are expected to evolve over time, laying a
strong structure is imperative; it’s much easier to start with a good structure
than to change it later.

The benefits laid out herein will be negligble, and may in fact cause
discomfort on a small scale. However, as the application grows in complexity
and dyanmism, the efforst will become appreciated.

###The Future
This framework hopes to advance the development of CSS architecture along the
same lines as the rest of the web.
[Web Components](http://www.w3.org/TR/components-intro/), and projects like
[Ember](http://emberjs.com/guides/components/),
[Angular](https://angularjs.org/) and
[Polymer](http://www.polymer-project.org/) are helping to teach developers the
power of modularized HTML, and this framework hopes to do the same with CSS.

###Inspiration
Inspiration for this framework comes from methodologies such as
[OOCSS](http://oocss.org/), [SMACSS](http://smacss.com/),
[BEM](http://bem.info/) and
[Atomic Design](http://bradfrostweb.com/blog/post/atomic-web-design/). Writing
this framework has meant humbly standing on the shoulders of giants like
[Nicole Sullivan](http://www.stubbornella.org/content/),
[Nicolas Gallagher](http://nicolasgallagher.com/),
[Jonathan Snook](http://snook.ca/) and
[Harry Roberts](http://csswizardry.com/). This framework exists because of
their efforts and leadership.

##Approach
This framework sets out to achieve clearly outlined goals. A few guiding
principles and the appropriate methods for following those principles have been
created in order to reach the goals laid out.

###Goals
- To facilitate effective scaling for larger projects
- Be cognizant of performance impacts
- Create minimal developer frustration
- Work towards ensuring speedy development time
- Hold true to flexibility, adaptabality and maintainability

###Principles
####Recycled Modularity
At it's core, this framework is a set of modularized components that can be
treated as building blocks for a larger web layout. In this framework,
modularity has four main characteristics: it is singularly responsible,
self-contained, decoupled and location independent.

#####_Singularly Responsible:_
A component should have a tightly defined role. It should only care about the
responsibilities defined by that role. CSS has many different rule sets.
Creating singularly responsible components means that you shouldn't have a
component that sets rules for positioning, text styles and element styles. That
is too much crossover and leads to brittle stylesheets and eventually spaghetti
code. A good way of achieving singular responsibility is by seperating style
from structure.

#####_Self Contained:_
A component should be strongly self contained. We should rely on strict scoping
in order to achieve this. That is, a component's elements should belong only to
that component. By preventing elements from reaching out of their component,
we're ensuring that the component can be easily shifted around without
impacting other component elements or its own elements. This also leads to a
leaner architecture that is easier to reason through, allowing developers to
predictiably make adjustments and more easily build up an application. There
are also performance benefits that come from not cascading the stylesheet.

#####_Decoupled:_
By writing small, independent components, we create objects that can be re-used
accross an application in a highly flexible manner. In doing so, we're writing
not only scalable stylesheets, but stylsheets that are easier to maintain
because they can be refactored or edited without affecting other components and
thus the layout. It is important to remember that many small components are
easier to decouple from one another than a few larger ones. You can build many
different types of houses with thousands of tiny bricks, but only a few with a
handful a gigantic stones.

#####_Location Independent:_
Components shouldn't be tied to HTML elements or it's structure within the DOM.
It should be able to shift from one location to another, and react in a
predictable manner. A well architected system has components that can be
assembled in various combinations and in various settings without problem. For
example, a `.nav` component shouldn't care if it has a `.breadcrumbs`
component, and that `.breadcrumbs` component shouldn't know or care about its
parent `.nav` component. Further, that `.nav` component should work just as
well being a `nav` or `ul` HTML element.

####Upward Consistency
Upward consistency describes a way to layer the styles in your CSS. It's main
tasks are to develop pattern repetition and encourage code reuse. In order to
establish upward consistency, a broad base that sets up non-classed elements
should be created. Avoid setting styles to HTML tags as much as possible, and
instead rely on the base to properly set up a foundation for component
building. For this framework, we're relying on
[Normalize](http://necolas.github.io/normalize.css/) to serve as our base.

Once a good base is set, we'll follow an organic hierarchy that works opposite
to inheritance-driven CSS. Traditional inheritence CSS forces us to write
selectors such as `.home .sidebar ul`. This creates a problem when we want to
take the component represented by the `ul` and place it somewhere else in our
application, or when we want to refactor that component without impacting the
rest of the page. So, instead of thinking in terms of descending selectors, we
should instead be thinking in an organic manner: a group of elements create a
component, a group of components create a layout, and a group of layouts create
a page. This could be represented in this manner
`Page < Layout < Component < Element`. This means that we no longer have to
consider the location or ancestry of a component when working with it, and so
are free to make it flexible and independent.

Thinking organically means we should be writing stylesheets that lead to
minimal overwriting of rules. Because we're working form the bottom up, and our
components are lean and independent, we should almost always be layering on
styles instead of overwriting. If you find yourself redefining rules on a
component, you should re-evaluate if your component is properly constructed
and make sure your're working organically.

####Ease of Consumption
Many important web frameworks have proved to be incredibly succesfull by
creating a set of conventions that helped guide the developer down the right
path. While it is good to think freely, a set of guidelines ensures that the
goals of the framework are always in focus.

With that in mind, this framework is opinionated as necessary. There are
conventions surrounding file organization and class naming. Heavy in-code
documentation based on JSDoc syntax is expected throughout, and a detailed
style guide should be followed as closely as possible.

While a slight learning curve is expected, the conventions baked into this
framework promote faster and easier future development while being as closely
aligned with the goals described above as possible.

##Conventions
###File Organization
Files should be be broken apart into small, coherent partials that mimic the
principles of modularity. This means small partials that consist of a
component, its elements and component modifiers. Five distinct partial types
should emerge: base partials, component partials, utility partials, helper
partials and theme partials. Utilities are low-level abstractions that can be
applied to any HTML element. Helpers are functions that provide pre-processing,
such as mixins. They typically provide positional styles or general
composition. Themes are styles that directly relate to how an HTML element
should look, and so sit on top of this framework. True themes are not included
as part of this framework, but a consistent expectation for how they should be
organized is important nevertheless.

The base class should be stored in the `base/` directory; components in the
`components/` directory; and utilities in the `utilities/` directory. Any
theme-related styles should be stored in directories that match the view they
are theming. For example, themes for the user profile of an application should
be kept in the `user_profile/` directory. Helpers, including mixins, variables
and functions should be kept in the `helpers/` directory.

All partials should be prefixed with an underscore and brought into the
sub-main stylesheets with `@import` declarations. Those sub-main stylesheets
should then be brought into the main stylesheet using `@import`.

A standard file structure within the stylesheets directory would closely
resemble the following:

```
|-- stylesheets/
  |
  |-- base/
  | |
  | |-- _base.scss
  |
  |-- components/
  | |
  | |-- _components.scss
  |
  |-- helpers/
  | |
  | |-- _helpers.scss
  |
  |-- themes/
  | |
  | |-- _themes.scss
  |
  |-- utilities/
  | |
  | |-- _utilities.scss
  |
  |-- main.scss
```

###Class Names
All class names in HTML and CSS are global objects. There is no way to
namespace a class, so this framework sets a defined naming convention to create
digestable class relationships and maintain low specificity, which is necessary
for an organic hierarchy. The rules are:

- All component names are `camelCased`
- A double dash `--` signifies a component modifier
  - A state modifiers are prefixed with `is-`
  - Utility classes are prefixed with `u-`
- Component elements are scoped to the component with a single dash
`component-element`

###Documentation
Good documentation helps to keep everyone working on a project happy. It's
important that all the developers know how a component works, any limitations
it might have and how modifiers should be applied. Additional notes on a
component, such as deprecation warnings, should be documented as well.

This framework follows a documentation practice based on JSDoc. After the
component title, a two to three sentence description of the component follows.
This description usually mentions the HTML elements the component is best
applied to, how it can be rationally used and the default styles. Regular
component classes are followed by example HTML markup.

Inline comment refrence points are the final point of the first documentation
block. These numbers correspond to specific points in your CSS rules that
deserve a note. Think of them as header notes.

A `NOTES` block may optionally follow the main documentation block. Notes may
include warnings or comments left for developers who may look at the component
in the future.

There is no need to note the author of a component.

Here's an example of what the component documentation might look like:
```scss
/**
 * Component nav
 *
 * A nav component that is best applied to `ul`, `ol` and `nav` elements.
 * Can be used for menus, headers, footers, sidebars, breadcrumbs and tabs.
 * Defaults to horizontally laid items with `.nav-item` children displayed
 * `inline-block`.
 *
 * <ul class="nav [nav--*]">
 *   <li class="nav-item">
 *     <a href="#">Home</a>
 *  </li>
 *   <li class="nav-item">
 *     <a href="#">About</a>
 *   </li>
 *   <li class="nav-item">
 *     <a href="#">Contact</a>
 *   </li>
 * </ul>
 *
 * 1. Removing any `ul` or `ol` inherited styles.
 * 2. Older browers don't support display `inline-block`, so the *display
 *    applies display `inline` only to IE and forces it to behave like
 *    `inline-block` by applying a zoom to the element.
 */

/**
 * NOTES
 * - This component includes JavaScript interactivity that can be found in the
 *   `js/components/nav.js` file.
 */
```

##Components
```scss
.componentName {
  // styles
}
```
```html
<div class="componentName">
  <!-- markup -->
</div>
```

###Component Element
A component element is a class that is scoped to a component. It's responsible
for applying styles directly to elements that sit within a component. They can
be thought of as sub-components, becuase they only make sense in the context of
the parent component. The syntax follows camel casing and all elements should
be prefixed with the component name and a dash.
```scss
.componentName-elementName {
  // styles
}
```
```html
<div class="componentName">
  <div class="componentName-elementName">
    <!-- markup -->
  </div>
</div>
```

###Component Modifier
A component modifier is a class that alters the styles of the main component.
The syntax follows camel casing and all modifiers should be prefixed with the
component name and a double dash. **The modifier class should be included in
the HTML in addition to the base component class.**

Modifier classes must have additional documentation describing how they modify
the main component.

```scss
/**
 * Modifier componentName--modification
 *
 * A description of the modifier.
 *
 * 1. An inline documentation reference points.
 */

.componentName--modification {
  // styles
}
```
```html
<div class="componentName componentName--modification">
  <!-- markup -->
</div>
```

Multiple modifier classes can be applied at once to construct structure.
```html
<div class="componentName componentName--modification componentName--modificationTwo">
  <!-- markup -->
</div>
```

###Component State Modifier
A component state modifier is a special type of modifier class that adds styles
to a component that is a particular state, such as an error state.

Be cautious when styling a state modifier on its own, and try to limit the
number of styles being applied; make sure they would make sense on any
component without compromising that component's own styles. The recommended
approach is to use the same state name in multiple contexts as an adjoining
class, while allowing the component to define its own styles for the state.
```scss
.componentName {
  &.is-atState {
    // styles
  }
}
```
```html
<div class="componentName is-atState">
  <!-- markup -->
</div>
```

##Utilities
```scss
.u-utilityName {
  // styles
}
```
```html
<div class="u-utilityName">
  <!-- markup -->
</div>
```

Multiple utility classes can be applied at once to construct structure.
```html
<div class="u-utilityName u-utilityNameTwo">
  <!-- markup -->
</div>
```

##Example
An example of the class name conventions:
```html
<!-- everything is `camelCased` and a double dash signifies a modifier -->
<div class="pageHeading pageHeading--secondary">
  <h1 class="pageHeading-title pageHeading-title--small">Title Text</h1>
  
  <!-- component elements are scoped to the componenent -->
  <figure class="pageHeading-graphic">
    <img src="#" alt="Image">
  </figure>

  <ul class="nav nav--stacked">
    <li class="nav-item"></li>
    <li class="nav-item"></li>
    <li class="nav-item"></li>
  </ul>
</div>

<!-- component classes can be applied to different HTML elements -->
<nav class="nav">
  <span class="nav-item"></span>
  <span class="nav-item"></span>
  <span class="nav-item"></span>
</nav>

<!-- multiple modifiers can be used -->
<form action="#" class="form form--slim form--horizontal">
  <h1 class="form-title">Title goes here</h1>
  <input type="text">

  <!-- modifiers can be applied to elements as well -->
  <button type="submit" class="form-button form-button--positive">
    Submit
  </button>
  <button type="button" class="form-button form-button--negative">
    Cancel
  </button>

  <!-- state modifiers are prefixed with `is-` and utilities with `u-` -->
  <p class="form-message is-errored u-hidden"></p>
</form>
```
