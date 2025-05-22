# TBLL - Web Server ISTQB

## Goal

- Learn how to design a test plan through specifications so that the test plan can really achieve the `test objectives` (ref: ch 1.1.1)


### Mapping ISTQB Test Objectives to `h1spec`

| ISTQB Test Objective | How `h1spec` Supports This Objective |
|----------------------|---------------------------------------|
| **Evaluate work products such as requirements** | Uses RFC7230 as formal requirements; each section is mapped to corresponding test cases. Design and implementation of tests are derived from protocol specifications. |
| **Trigger failures and find defects** | no need to describe |
| **Ensure adequate coverage of the test object** | Defines coverage based on RFC section mapping (e.g., §3.1.1, §3.3.2). Coverage tracking is included to show tested vs. untested sections. |
| **Reduce the level of risk of inadequate software quality** | Focuses testing on high-risk areas (e.g., header parsing, chunked encoding, persistent connections). Prioritizes tests based on risk and impact. |
| **Verify whether specified requirements have been fulfilled** | Each test case includes the expected behavior according to the RFC. Failures are linked to specific violations of protocol requirements. |
| **Verify compliance with contractual, legal, and regulatory requirements** | Treats RFC7230 as a normative standard. `h1spec` becomes a tool for verifying protocol compliance and interoperability. |
| **Provide information for decision making** | Outputs structured test reports showing pass/fail status, RFC reference, and failure explanations, enabling informed decisions by stakeholders. |
| **Build confidence in the quality of the test object** | Encourages frequent automated regression runs. Reliable, repeatable tests improve trust in server implementation stability. |
| **Validate whether the test object is complete and works as expected by stakeholders** | Ensures that essential HTTP behaviors (e.g., correct status codes, persistent connection handling) are tested and validated based on real-world use cases. |

## What is the outcome of this project?

Have a tester which follow the ISTQB standard and can be used to test the HTTP/1.1 server.

## Next Steps

> Exhaustive testing is impossible. Testing everything is not feasible except in trivial cases (Manna 1978). Rather than attempting to test exhaustively, test techniques (see chapter 4), test case prioritization (see section 5.1.5), and risk-based testing (see section 5.2), should be used to focus test efforts

1. Need to read ch5 to understand how to prioritize the test cases