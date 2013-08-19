intuitive approach to testing that emphasizes the behavior of the application rather than its precise implementation, a variant of test-driven development (TDD) known as behavior-driven development (BDD). Our main tools will be integration tests (starting in this section) and unit tests (starting in Chapter 6). Integration tests, known as request specs in the context of RSpec, allow us to simulate the actions of a user interacting with our application using a web browser. Together with the natural-language syntax provided by Capybara, integration tests provide a powerful method to test our application’s functionality without having to manually check each page with a browser. (Another popular choice for BDD, called Cucumber, is introduced in Section 8.3.)



defining quality of TDD is writing tests first, before the application code. Initially, this might take some getting used to, but the benefits are significant. By writing a failing test first and then implementing the application code to get it to pass, we increase our confidence that the test is actually covering the functionality we think it is. Moreover, the fail-implement-pass development cycle induces a flow state, leading to enjoyable coding and high productivity. Finally, the tests act as a client for the application code, often leading to more elegant software designs.



In this section, we’ll be running the tests using the rspec command supplied by the RSpec gem. This practice is straightforward but not ideal, and if you are a more advanced user I suggest setting up your system as described in Section 3.6.



n test-driven development, we first write a failing test, represented in many testing tools by the color red. We then implement code to get the test to pass, represented by the color green. Finally, if necessary, we refactor the code, changing its form (by eliminating duplication, for example) without changing its function. This cycle is known as “Red, Green, Refactor”.




