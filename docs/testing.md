##Testing Components
Having robust tests decreases the number of defects in your application, as
well as encourages strong software design.

###JavaScript Unit Tests
Modularity goes hand in hand with proper unit testing because it inherently
forces you to isolate your test scenarios, a sign of good unit tests. When
writing unit tests, follow these guidelines:
- Create orthogonal (independent) tests
- Name your unit tests clearly and consistently
- Mock out external services and dependencies
- Test only one system at a time

###JavaScript Integration Tests
While unit tests provide a strong underlayer for testing individual modules,
integration tests make sure that the entire application is working properly on
a holistic level. Writing good integration tests is essential for
peace-of-mind.

If creating an application that depends on a data API, such as a RESTful set of
HTTP endpoints, it's important to test against the expected shape of data
responses. This prevents errors from ocurring due to a backend refactor or
change that the front-end may not have been aware of.

###CSS Visual Tests
Visual tests should be used when creating a new component with styles. This
brings some sanity to the crazy world of CSS bugs. Visual tests follow a
BDD-style markup, which makes it easy to identify the system under test.

####Test
Uses the `.test` class. Serves as a container for the visual test.

```html
<div class="test">
  ...
</div>
```

####Test Describe
Uses the `.test__describe` class. Creates an example group. The content after
this element are meant to be evaluted as text examples. A describe element can
hold other describe elements, context elements, it elements and assertions.
```html
<div class="test">
  <div class="test__describe">
    <h1>Some Component</h1>
    ...
  </div>
</div>
```

####Test Context
Uses the `.test__context` class. Provides additional context when within an
example group. While the purpose of describe is to wrap a set of tests against
one functionality, the purpose of context is to wrap a set of tests against one
functionality under the same state. When describing a context, start its
description with “when” or “with”.
```html
<div class="test">
  <div class="test__describe">
    <h1>Some Component</h1>
    <div class"test__content">
      <h2>When in one context</h2>
      ...
    </div>

    <div class"test__content">
      <h2>When in another context</h2>
      ...
    </div>
  </div>
</div>
```

####Test It
Uses the `.test__it` class. Describes a test. Should typically be no longer
than 40 characters long and use no conjunctions. If either of those is true,
consider using a context element to split the test.
```html
<div class="test">
  <div class="test__describe">
    <h1>Some Component</h1>
    <div class"test__it">
      <h2>It asserts something</h2>
      ...
    </div>
  </div>
</div>
```

####Test Assertion
Uses the `.test__assertion` class. Holds the actual component being tested as
described by the it element.
```html
<div class="test">
  <div class="test__describe">
    <h1>Some Component</h1>
    <div class"test__it">
      <h2>It asserts something</h2>
      <div class="test__assertion">
        <!-- render component -->
      </div>
    </div>
  </div>
</div>
```

####Visual Diffing
If you'd rather not have to always look at each visual test manually, this can
be hanlded by running the output of your visual tests through a visual diffing
tool that will detect when there are visual changes in your test suite.
