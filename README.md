# React UI testing with Capybara

Trying to wrap my head around the very large topic of UI testing, stemming from
using React/Om for building predictable UIs and Capybara for automated testing.

### Building UIs with React

[React] allows us to build UIs on the Web that are predictable, rendering the
DOM indirectly as a function of formally defined state, rather than allowing
direct ad-hoc mutation. [Om] takes this further by allowing us to consolidate
all of said state into a single place, making it easy to snapshot/reload state
of our entire app for debugging.

### Why write tests?

Technology like React may offset the importance of testing by increasing a
developer's confidence/speed in fixing bugs during development, but this is of
little consequence to teams that necessitate automated quality control. For
example, my team requires some form of tests that run to promote newly
committed code to an acceptance stage in a CI pipeline.

### What kind of tests CAN we write?

UI testing can be done at different levels.

We can write __code-level__ tests for units in isolation, or we can verify how
they work together.  For tests that rely on an external service, we can test
against it or a "mock" version.

We can also write __user-level__ tests that simulate what a user is doing and
expecting to see.  Simulating what a user is doing can be done at the input
level (e.g. clicking, typing), DOM level (e.g. finding elements, setting
values, triggering events), code level (calling UI functions directly), or
state level (setting UI state directly).

Verifying what a user sees can be at the screen level (e.g. bitmaps), DOM level
(e.g. finding elements, attributes), or state level (checking UI state
directly).

### What kind of tests SHOULD we write?

Natural language test scenarios allow product managers to be able to read and
verify acceptance criteria for UI features.  Making those scenarios executable
is beneficial for automated acceptance (e.g. via [Cucumber]).

These types of natural language testing encourages collaboration between
testers (QEs) and developers.  Both are able to write tests.

### How much testing?

Ideally, test coverage should be 100%. But practically, the amount of effort on
test coverage should be dependent on the confidence of the business value of a
given feature. If we are showing something to a customer to gauge its value,
tests are less important than if we were confident in exactly what they user
wants.

### Brittleness of tests

UI test fragility is easier to talk about when focusing on the fragility of the
components that comprise a page.  It seems components are fragile on two
separate levels: position and nature.

Its __position__ and other place-oriented details can change, causing us to
change our queries for locating/updating them.  But its __nature__ can also
change.  For example, its underlying component could disappear if its not
needed anymore or if its role fuses with another.

The position-type fragility can be addressed by creating Page Objects using
Site Prism, hiding position-level details from the test steps.  The nature-type
fragility is inherent to the problem of changing UI behavior.  Changes will
unavoidably have to be made across test steps and Page Objects.

- [discussion about testing difficulties and desires at PROS](https://www.yammer.com/pros.com/#/threads/inGroup?type=in_group&feedId=3931726)
- <http://www.cheezyworld.com/2010/11/09/ui-tests-not-brittle/>
- <http://burdettelamar.wordpress.com/2014/04/01/encapsulate-the-gui-tool/>
- <http://burdettelamar.wordpress.com/2014/03/21/keep-your-page-objects-dry/>
- <https://github.com/natritmeyer/site_prism>
- <https://code.google.com/p/selenium/wiki/PageObjects>
- <http://martinfowler.com/bliki/TestPyramid.html>
- <http://code.tutsplus.com/tutorials/tips-to-avoid-brittle-ui-tests--net-35188>
- <http://www.stickyminds.com/articles/fixing-brittleness-problem-gui-tests>
- <http://thoughtworks.github.io/p2/issue09/broken-ui-tests/>
- <http://programmers.stackexchange.com/questions/197096/using-only-ui-testing-is-that-ok>


### Can React help testing?

Since it seems that building Page Objects duplicates some data/logic we have in
the UI code, it may be possible to generate them based on our React Component
tree for our page.  This may decrease the brittleness of our code.

[React]:http://facebook.github.io/react/
[Om]:https://github.com/swannodette/om
