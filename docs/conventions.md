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
