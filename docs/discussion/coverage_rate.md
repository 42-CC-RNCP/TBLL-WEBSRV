
I have a question that’s not directly related to Testiny.io, but rather to how we should define “coverage rate” in the context of our project goals (see [mapping ISTQB test objectives to h1spec](https://github.com/42-CC-RNCP/TBLL-WEBSRV/blob/main/docs/project_plan_20250522.md#mapping-istqb-test-objectives-to-h1spec) and our scenario in [one page test plan](https://github.com/42-CC-RNCP/TBLL-WEBSRV/blob/main/docs/one_page_test_plan.md#-test-objectives-ref-istqb-511--purpose-of-testing-test-planning)).

We are confused about what coverage means in our situation.

#### The context and our thinking:

1. **The RFC protocol** defines the contract between a web server and client. If our implementation does not follow the spec, it introduces various risks.
2. **Traditional code coverage** (i.e., how much program logic was tested) does not necessarily reflect confidence that the implementation meets the protocol requirements. As ISTQB states, one purpose of testing is to *increase confidence*. Ideally, we’d like our test coverage metric to reflect how confident we can be that the implementation meets the RFC.
3. **It’s impossible to define all possible test cases** for a non-trivial protocol.

So we considered an alternative definition:

* Assume that “coverage rate” is the ratio of RFC chapters (or major requirements) for which we have at least one test case implemented.
  For example, if the RFC has 10 chapters and we wrote test cases for 5 of them, coverage rate = 5 / 10.
* If all test cases for those chapters pass, then we have coverage—and confidence—at that level, even if we haven’t covered every single detail in the RFC.

#### My questions:

* Is this a reasonable approach to define coverage in this context?
* Or is the idea of “coverage rate” not meaningful at all for this type of requirements-based (RFC-driven) testing?
* Would you suggest a better way for a small team with limited resources to express and manage “confidence” in their conformance testing?
