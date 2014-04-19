#Spot CSS Framework
> A modern day CSS framework that follows a flexible approach for creating scalable stylesheets.

##Introduction
Cascading stylsheets were built to be used on sites that are very different from the web applications that we're currently building. This dictates the need to abandon the traditional way of styling webpages, and implement a framework that mirrors the way applications are programatically architected. That is, we should borrow from other web domains, and apply those best practices to web design: modularity, a separation of concerns, DRY, encapsulation, convention, etc.

###Difficulties
On smaller/short-lived projects, it's often okay to not worry about scalablity and how the current approach will impact future design and development. However, on web applications that are expected to evolve over time, laying a strong structure is imperative; it’s much easier to start with a good structure than to change it later.

The benefits laid out herein will be negligble, and may in fact cause discomfort on a small scale. However, as the application grows in complexity and dyanmism, the benefits will increase exponentially.

##Approach
This framework sets out to achieve clearly outlined goals. A few guiding principles and the appropriate methods for following those principles have been created in order to reach the goals laid out.

###Goals
- Facilitate effective scaling for larger projects
- Be cognizant of performance impacts
- Create minimal developer frustration
- Work towards ensuring speedy development time
- Hold true to flexibility, adaptabality and maintainability

###Principles
####Recycled Modularity
At it's core, this framework is a set of modularized components that can be treated as building blocks for a larger web layout. In this framework, modularity has four main characteristics: it is singularly responsible, self-contained, decoupled and location independent.
#####_Singularly Responsible:_
A component should have a tightly defined role. It should only care about the responsibilities defined by that role. CSS has many different rule sets. Creating singularly responsible components means that you shouldn't have a component that is sets rules for positioning, text styles and element styles. That is too much crossover and leads to brittle stylesheets and eventually spaghetti code. A good way of achieving singular responsibility is by seperating style from structure.

#####_Self Contained:_
A component should be strongly self contained. We should rely on strict scoping in order to achieve this. That is, a component's elements should belong only to that component. By preventing elements from reaching out of their component, we're ensuring that the component can be easily shifted around without impacting other component elements or its own elements. This also leads to a leaner architecture that is easier to reason through, allowing developers to predictiably make adjustments and more easily build up an application.

#####_Decoupled:_
By writing small, independent components, we create modules that can be re-used accross an application in a highly flexible manner. In doing so, we're writing not only scalable stylesheets, but stylsheets that are easier to maintain because they can be refactored or edited without affecting other components and thus the layout. It is important to remember that many small components are easier to decouple from one another than a few larger ones. You can build many different types of houses with thousands of tiny bricks, but only a few with a handful a gigantic stones.

#####_Location Independent:_
Make sure not to tie your components to an HTML element or it's structure with the DOM. It should be able to shift from one location to another, and react in a predictable manner. A well architected system has components that can be assembled in various combinations and in various settings without problem. For example, a `.nav` component shouldn't care if it has a `.breadcrumbs` component, and that `.breadcrumbs` component shouldn't know or care about its parent `.nav` component. Further, that `.nav` component should work just as well with an `aside` element as a `ul`.

####Upward Consistency
Upward consistency describes a way to layer the styles in your CSS. It's main taks are to develop pattern repetition and encourage code reuse. In order to establish upward consistency, we create a broad base that sets up non-classed elements. We should avoid setting styles to HTML tags as much as possible, and instead rely on the base to properly set up a foundation for component building. For this framework, we're relying on [Normalize](http://necolas.github.io/normalize.css/) to serve as our base.

Once a good base is created, we'll follow an organic hierarchy that works opposite to inheritance-driven CSS. Traditional inheritence CSS forces us to write selectors such as `.home .sidebar ul`. This creates a problem when we want to take the component represented by the `ul` and place it somewhere else in our application, or when we want to refactor that component without impacting the rest of the page. So, instead of thinking in terms of descending selectors, we should instead be thinking in an organic manner: a group of elements create a component, a group of components create a layout, and a group of layouts creates a page. This could be represented in this manner `Page < Layout < Component < Element`. This means that we no longer have to consider the location or ancestry of a component when working with it, and so are free to make it flexible and independent.

Thinking organically means we should be writing stylesheets that lead to minimal overwriting of rules. Because we're working form the bottom up, and our components should be lean and independent, we should almost always be layering on styles instead of overwriting. If you find yourself redefining rules on a component, you should re-evaluate if your components are properly constructed and make sure your're working organically.

####Ease of Consumption
Many important web frameworks have proved to be incredibly succesfull by creating a set of conventions that helped guide the developer down the right path. While it is good to think freely, a set of guidelines ensures that the goals of the goals of the framework are always in focus.

With that in mind, this framework is opinionated as necessary. There are conventions surrounding file organization and class naming. Heavy in-code documentation based on JSDoc syntax is expected throughout, and a detailed style guide should be followed as closely as possible.

While a slight learning curve is expected, the conventions baked into this framework promote faster and easier future development that is as closely aligned with the goals initially set as possible.

##Conventions
###File Organization
Files should be be broken apart into small, coherent partials that mimic the principles of modularity. This means small partials that consist of a component, its elements and component modifiers. Four distinct partial types should emerge: base partials, component partials, utility partials and theme partials. Utilities are low-level abstractions that can be applied to any HTML element. They typically provide positional styles or general composition. Themes are styles that directly relate to how an HTML element should look, and so sit on top of this framework. Themes are not included as part of this framework, but a consistent expectation for how they should be organized is important nevertheless.

The base class should be stored in the `base/` directory; components in the `components/` directory; and utilities in the `/utilities` directory. Any theme-related styles should be stored in directories that match the view they are theming. For example, themes for the user profile of an application should be kept in the `user_profile/` directory.

All partials should be prefixed with an underscore and brought into the main stylesheet with `@import` declarations.

A standard file structure within the stylesheets directory might look like this:

###Class Names
All class names in HTML and CSS are global objects. There is no way to namespace a class, so this framework sets a defined naming convention to create digestable class relationships and maintain low specificity, which is necessary for an organic hierarchy. The rules are:

- All component names are `camelCased`
- A double dash `--` signifies a component modifier
- A state modifier is prefixed with `is` and is an adjoining class
- Utility classes are prefixed with `u-`
- Component elements are scoped to the component with a single dash `component-figure`
- Nested components may optionally be wrapped in HTML element with a prefixed class `component w-nestedComponent`

###Documentation
Good documentation helps to keep everyone working on a project happy. It's important that all the developers know how a component works, any limitations it might have and how modifiers should be applied. Additional notes on a component, such as deprecation warnings, should be documented as well.

This framework follows a documentation practice based on JSDoc. After the component title, a two to three sentence description of the component follows. This description usually mentions the HTML elements the component can be applied to, how it can be rationally used and the default styles. Regular component classes are followed by example HTML markup.

Inline comment refrence points are the final point of the first documentation block. These numbers correspond to specific points in your CSS rules that deserve a note. Think of them as header notes.

A `NOTES` block may optionally follow the main documentation block. Notes may include warnings or comments left for developers who may look at the component in the future.

There is no need to note the author of a component or it's version.

Here's an example of what the component documentation might look like:
```scss
/**
 * Component nav
 *
 * A navigation component that is best applied to `ul`, `ol` and `nav` elements.
 * This component can be used for menus, headers, footers, sidebars, breadcrumbs and tabs.
 * By default it is horizontally laid item with `.nav-item` children displayed `inline-block`.
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
 * 2. Older browers don't support display `inline-block`, so the *display applies
 *    display `inline` only to IE and forces it to behave like `inline-block` by
 *    applying a zoom to the element.
 */

/**
 * NOTES
 * - This component was modified from an earlier version. That version can be accessed in the `deprecations` directory.
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
A component element is a class that is scoped to a component. It's responsible for applying styles directly to HTML elements that sit within a component. The syntax follows camel casing and all elements should be prefixed with the component name and a dash.
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
A component modifier is a class that alters the styles of the main component. The syntax follows camel casing and all modifiers should be prefixed with the component name and a double dash. **The modifier class should be included in the HTML in addition to the base component class.**

Modifier classes must have additional documentation describing how they modify the main component.

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
A component state modifier is a special type of modifier class that adds styles to a component that is an a particular state, such as an error state. These classes typically get added using Javascript. State modifiers can be applied to all components, but each component should style its own state modifiers. **State modifiers should only be styled as adjoining classes.**
```scss
.componentName {
  &.isAtState {
    // styles
  }
}
```
```html
<div class="componentName isAtState">
  <!-- markup -->
</div>
```

###Nesting Components
If you're nesting components it may be beneficial to wrap it an HTML element. If so, the wrapper element should have and two classes applied to it: the outer components name and the inner components name prefixed by a `w-`.
```html
<div class="component w-anotherComponent">
  <div class="anotherComponent">
    <!-- markup -->
  </div>
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
<div class="pageHeading pageHeading--secondary"> <!-- everything is camelCased and a double dash signifies a component modifier -->
  <h1 class="pageHeading-title pageHeading-title--small">Title Text</h1>
  <figure class="pageHeading-graphic"> <!-- component elements are scoped to the componenent -->
    <img src="#" alt="Image">
  </figure>
  <div class="pageHeading w-nav"> <!-- when nesting a component inside of another, you may need to wrap it with a w- class -->
    <ul class="nav nav--stacked">
      <li class="nav-item"></li>
      <li class="nav-item"></li>
      <li class="nav-item"></li>
    </ul>
  </div>
</div>

<nav class="nav"> <!-- component classes can be applied to different HTML elements -->
  <ul>
    <li class="nav-item"></li>
    <li class="nav-item"></li>
    <li class="nav-item"></li>
  </ul>
</nav>

<form action="#" class="form form--slim form--horizontal"> <!-- multiple modifiers can be used -->
  <h1 class="form-title">Title goes here</h1>
  <input type="text">
  <button type="submit" class="form-button form-button--positive">Submit</button>
  <button type="button" class="form-button form-button--negative">Cancel</button>
  <p class="form-message is-errored u-hidden"></p> <!-- state classes are prefixed with is- and utility with u- -->
</form>
```
