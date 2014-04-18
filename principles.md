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
- Pattern repetition and code reuse
- Crete a broad base that sets up non-classed elements
- Set an organic hierarchy that works opposite to inheritance-driven CSS
    Elements -> Components -> Layouts -> Pages
- Progressive style layering (no overwriting styles)


####Ease of Consumption
- Slight learning curve, that promotes faster and easier future development
- Defining naming and file organization conventions (opinionated as necessary)
- Heavy in-code documentation
- Detailed style guide


