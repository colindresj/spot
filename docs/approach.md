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
