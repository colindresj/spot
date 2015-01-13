#Spot CSS Framework
> A modern day component-based framework that follows a flexible approach to
  creating scalable front-ends.

##Introduction
HTML, CSS and JavScript were built to be used on sites that are very different
from the web applications that we're currently building. This dictates the
need to abandon the traditional way of creating webpages, and implement a
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
and dyanmism, the efforts will gradually be more appreciated.

###The Future
This framework hopes to advance the development of front-end architecture along
the same lines as much of the web is already going. Many projects are helping
to teach developers the power of modularized code, and this framework hopes to
serve as a base implemenetation and set of conventions of that approach,
specifically for the front-end.

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
a modular component has four main characteristics: it is singularly responsible,
self-contained, decoupled and location independent.

#####_Singularly Responsible:_
A component should have a tightly defined role. It should only care about the
responsibilities defined by that role. For example, CSS has many different rule
sets.  Creating singularly responsible components means that you shouldn't have
a component that sets rules for positioning, text styles and element styles.
That is too much crossover and leads to brittle stylesheets and eventually
spaghetti code. A good way of achieving singular responsibility is by
seperating style
from structure.

#####_Self Contained:_
A component should be strongly self contained. We should rely on strict scoping
in order to achieve this. That is, a component's elements should belong only to
that component. By preventing elements from reaching out of their component,
we're ensuring that the component can be easily shifted around without
impacting other component elements or its own elements. This also leads to a
leaner architecture that is easier to reason through, allowing developers to
predictiably make adjustments and more easily build up an application. Their
concern is the public API (input/output), not the internals of a particular
component. There are also performance benefits that come from not cascading the
stylesheet or polluting namescapes.

#####_Decoupled:_
By writing small, independent components, we create objects that can be re-used
accross an application in a highly flexible manner. In doing so, we're writing
not only scalable front-ends, but stylsheets and scripts that are easier to
maintain because they can be refactored or edited without affecting other
components and thus the larger application. It is important to remember that
many small components are easier to decouple from one another than a few larger
ones. You can build many different types of houses with thousands of tiny
bricks, but only a few with a handful a gigantic stones.

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
building. This framework, relies on an extension of
[Normalize](http://necolas.github.io/normalize.css/) to serve as its base.

Once a good base is set, follow an organic hierarchy that works opposite to
inheritance-driven CSS. Traditional inheritence CSS forces us to write
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
declarations instead of overwriting. This could be thought of as extension over
modification.

If you find yourself redefining rules on a component, you should
re-evaluate if your component is properly constructed and make sure your're
working organically.

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
Files should be be broken apart into small, coherent component directores that
mimic the principles of modularity. This means small directories that contain
everything about a component.

A component directory contains the associated main HTML, CSS and JavaScript.
Additional files can be placed in a `lib/` directory; behavior, visual and unit
tests in the `tests/` directory; and text files denoting authors/maintainers, a
changelog, etc.

In addition to components, this framework outlines four additional CSS-specific
modules that can exist: base partials, utility partials, helper partials and
theme partials.

Utilities are low-level global style abstractios that can be applied to any
HTML element. Helpers  are functions that leverage language pre-processing and
post-processing, such as mixins. Themes are styles that directly relate to how
an HTML element should look, and so sit on top of this framework.

All these partials shit sit within a `common-stylesheets` directory, denoting
their global use. Within this directory, base partials should be stored in the
`base/` directory; components in the `components/` directory; utilities in the
`utilities/` directory; helpers in the `helpers/` directory; and themes in the
`themes/` directory.

Themes should contain a sibling partial for defining variable overrides. It's
important to understand that these overrides do not cancel out a particular
declaration, they simply replace the value of the variable before it is
transpiled to browser-ready CSS. __It's critical to know why this is ok, while
true declaration overriding is not__.

A standard file structure within the client directory would closely
resemble the following:

```
  client
    ├── assets
    ├── common-stylesheets
      ├── base
      ├── helpers
      ├── themes
        ├── some-theme.css
        └── some-theme.overrides.css
      └── utilities
    ├── components
      ├── some-component
      ├── some-other-component
        ├── lib
        ├── test
        ├── index.css
        ├── index.html
        ├── index.js
        └── AUTHORS.md
        └── CHANGELOG.md
      └── some-third-component
```

###Documentation
Good documentation helps to keep everyone working on a project happy. It's
important that all the developers know how a component works, any limitations
it might have and how modifiers should be applied. Additional notes on a
component, such as deprecation warnings, should be documented as well.

This framework follows a documentation practice based on JSDoc for JavaScript,
and a similar markup for CSS.

For CSS, After the component title, a two to three sentence description of the
component follows. This description usually mentions the HTML elements the
component is best applied to, how it can be rationally used and the default
styles. Regular component classes are followed by example HTML markup.

Inline comment refrence points are the final point of the first documentation
block. These numbers correspond to specific points in your CSS rules that
deserve a note. Think of them as header notes.

Here's an example of what the component documentation might look like for a CSS
file:

```css
/**
 * @component Nav
 *
 * @description
 * A nav component that is best applied to `ul`, `ol` and `nav` elements.
 * Can be used for menus, headers, footers, sidebars, breadcrumbs and tabs.
 * Defaults to horizontally laid items with `.nav-item` children displayed
 * `inline-block`.
 *
 * @example
 * <ul class="nav [nav--*]">
 *   <li class="nav__item">
 *     <a href="#">Home</a>
 *   </li>
 *   <li class="nav__item">
 *     <a href="#">About</a>
 *   </li>
 *   <li class="nav__item">
 *     <a href="#">Contact</a>
 *   </li>
 * </ul>
 *
 * @inline
 * 1. Removing any `ul` or `ol` inherited styles.
 * 2. Older browers don't support display `inline-block`, so the *display
 *    applies display `inline` only to IE and forces it to behave like
 *    `inline-block` by applying a zoom to the element.
 */
```

Standard [JSDoc](http://usejsdoc.org/) syntax applies for documenting
JavaScript files.

For the most part, HTML should not need documentation as it's just a markup
layer.

###Class Names
All class names in HTML and CSS are global objects. There is no way to
namespace a class, so this framework sets a defined naming convention to create
digestable class relationships and maintain low specificity, which is necessary
for an organic hierarchy. The rules closely resemble BEM, and are:

- All component names are hyphen delimited `some-component`
- Subcomponents are scoped to the component with a double underscore
  `some-component__child-component`
- A double dash signifies a component modifier
  `some-component.some-component--modified`
- An optional namespace be prepended to component classes
- Component states can be set with an “is-” prefix `some-component.is-<state>`
- Utility classes are prefixed with “u-” prefix `u-<utility-name>`

Component class syntax can be summarized as:
`[<namespace>-]<component-name>[--modifier|__child-component] [is-<state>]`

Utility class syntax can be summarized as:
`u-<utility-name>`

####Components
```css
.some-component {
  ...
}
```

```html
<div class="some-component">
  ...
</div>
```

#####Namespace
An optional namespace can be used as a prefix. This may help if you want to
prevent potential collisions between CSS libraries.

```css
.ns-some-component {
  ...
}
```

```html
<div class="ns-some-component">
  ...
</div>
```

#####Child Components
A child component is scoped to another component. It's responsible for applying
styles directly to HTML elements that sit within a component. They can be
thought of as sub-components. They should only make sense in the context of the
parent component and should not be exposed or accessible by other components.
In this way, you can think of them as private.

```css
.some-component__sub-component {
  ...
}
```

```html
<div class="some-component">
  <div class="some-component__sub-component">
    ...
  </div>
</div>
```

#####Component Modifiers
A component modifier is a class that alters the styles of the main component.
**The modifier class should be included in the HTML in addition to the base
component class.**

Modifier classes must have additional documentation describing how they modify
the main component.

```css
/**
 * @modifier some-component--modifier
 *
 * @description
 * A description of the modifier.
 *
 * @inline
 * 1. An inline documentation reference point.
 */

.some-component--modification {
  ...
}
```

```html
<div class="some-component some-component--modifier">
  ...
</div>
```

Multiple modifier classes can be applied at once to construct structure.

```html
<div class="some-component some-component--modifier some-component--modifier-two">
  ...
</div>
```

#####Component States
Component states, such as error states, can be styled using a class prefixed
with “is-”.

Be cautious when styling a state modifier on its own, and limit the number of
styles being applied; make very sure they would make sense on any component
without compromising that component's own styles. The recommended approach is
to use the same state name in multiple contexts as an adjoining class, while
allowing the component to define its own styles for the state.

```css
.some-component.is-at-state {
  ...
}
```

```html
<div class="some-component is-at-state">
  ...
</div>
```

####Utilities
```css
.u-some-utility {
  ...
}
```

```html
<div class="u-some-utility">
  ...
</div>
```

Multiple utility classes can be applied at once to construct structure.
```html
<div class="u-some-utility u-another-utility">
  ...
</div>
```
