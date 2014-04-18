#Spot CSS Framework
> A modern day CSS framework that follows a flexible approach for creating scalable stylesheets.

##Introduction
Cascading stylsheets were built to be used on sites that are very different from the web applications that we're currently building. This dictates the need to abandon the traditional way of styling webpages, and implement a framework that mirrors the way applications are programatically architected. That is, we should borrow from other web domains, and apply those best practices to web design: modularity, a separation of concerns, DRY, encapsulation, convention, etc.

###Difficulties
On smaller/short-lived projects, it's often okay to not worry about scalablity and how the current approach will impact future design and development. However, on web applications that are expected to evolve over time, laying a strong structure is imperative; it’s much easier to start with a good structure than to change it later.

The benefits laid out herein will be negligble, and may in fact cause discomfort on a small scale. However, as the application grows in complexity and dyanmism, the benefits will increase exponentially.

##Approach
###Goals
- Effectively scale for larger projects
- Recognize performance
- Create minimal developer frustration
- Speed up development time
- Maintain flexibility, adaptabality and maintainability

###Themes
- Modularity
  - Reusable
  - Singularly responsible
  - Highly decoupled and self-contained
  - Location independent
- Consistency
- Ease of consumption
  - Slight learning curve, that promotes faster and easier future development
- Pattern repetition and code reuse

###Methods
- Broad base that sets up non-classed elements
- An organic hierarchy (opposite of inherited CSS)
    Elements -> Components -> Layouts -> Pages
- Progressive style layering (no overwriting styles)
- Strict component scoping
- Seperate appearence from structure
- Defining naming and file organization conventions (opinionated as necessary)
- Heavy in-code documentation
- Detailed style guide
