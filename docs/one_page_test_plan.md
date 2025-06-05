# One-Page Test Plan for Web Server Testing

## 📌 Test Objectives *(Ref: ISTQB 5.1.1 – Purpose of Testing, Test Planning)*
1. Verify that the Web Server operates stably and does not crash when handling valid and invalid HTTP requests.
2. Ensure that server behavior conforms to the RFC HTTP/1.1 specification, including request-line, headers, body handling, and transfer encoding.
3. Support regression testing to ensure that new features or code changes do not break existing functionality.
4. Establish an automated, risk-based testing process using `h1spec` to ensure maintainability and reproducibility.

### Assumptions & Constraints
- Development and testing are conducted by a 3-person team.
- Testing must fit into limited hardware: 1 CPU, 4GB RAM, 20GB disk.
- Project follows a waterfall model; testing starts after implementation is complete.
- No external test automation tools or commercial CI infrastructure budgeted.

### Stakeholders
| Role         | Responsibility                      |
|--------------|--------------------------------------|
| Developer A  | Protocol logic, test case design     |
| Developer B  | Infrastructure, CI integration       |
| Developer C  | CGI logic, chunked encoding support  |

### Communication
- Weekly summary meetings
- Issues and Test Results tracked using GitHub Issues + Testiny.io
- Markdown-based documentation stored in repo `/docs`


### Metrics to Be Collected
- Pass/fail counts by priority (P0, P1, P2…)
- RFC section coverage %

### Budget & Schedule
- No monetary budget; open-source internal project
- Testing phase duration: 4 weeks

---


## 📦 Test Items (Scope In) *(Ref: ISTQB 5.1.2 – Test Items and Scope Definition)*
- Supports HTTP methods: GET / POST / DELETE
- Handles request-line, headers, body (including chunked encoding)
- Returns correct HTTP status codes (e.g., 200, 400, 404)
- Correctly handles chunked transfer encoding and file uploads
- Supports CGI execution
- Supports persistent connections (keep-alive)
- Load and performance testing (e.g., 1000+ concurrent connections) will be conducted

## 🚫 Out of Scope *(Ref: ISTQB 5.1.2 – Test Scope and Out-of-Scope Items)*
- No support for HTTPS / TLS encryption
- No support for HTTP/2 or later
- Does not validate third-party CGI behavior (only server-side invocation is tested)

---

## 🚨 Risk-Based Test Prioritization *(Ref: ISTQB 5.2 – Risk Management)*
| Functional Area              | Potential Risk                                                              | Impact                              | Urgency                                | Priority |
| ---------------------------- | --------------------------------------------------------------------------- | ----------------------------------- | -------------------------------------- | -------- |
| **Request-line parsing**     | Malformed format causes desynchronization → all subsequent requests fail    | **Extensive** (system-wide failure) | **Immediate** (common source of error) | **P0**   |
| **Request processing (OOM)** | e.g., extremely long headers cause memory overflow and server crash         | **Extensive** (crash)               | **High** (likely under load)           | **P0**   |
| **Chunked encoding**         | Incorrect chunk endings → infinite wait, decoding error, resource waste     | **Large** (functional degradation)  | **Moderate**                           | **P0**   |
| **CGI failure handling**     | Fails to return 502 or server blocks on CGI response                        | **Moderate**                        | **Moderate**                           | **P2**   |
| **File upload**              | No size or format validation → server slowdown or failure due to large file | **Moderate**                        | **Moderate**                           | **P2**   |
| **Persistent connections**   | Keep-alive not released → resource leak over time                           | **Minor**                           | **Low**                                | **P3**   |
| **High-load simulation**     | 1000+ concurrent connections may cause packet drops, hangs, memory leaks    | **Extensive**                       | **High**                               | **P1**   |

---

## ✅ Test Criteria *(Ref: ISTQB 5.1.6 – Exit Criteria; 5.3 – Test Monitoring and Control)*
**Entry Criteria**
- Web Server can start and accept basic HTTP requests
- CI/CD environment (GitHub Actions) is fully configured
- `h1spec` test framework is operational

**Exit Criteria**
- All **P0** priority tests have passed
- All **P1** tests have been executed and logged
- All detected P0-level defects have been fixed and re-tested
- Test report successfully submitted to Testiny.io and logged via CI

---

## ⚙️ Test Environment & Tooling *(Ref: ISTQB 5.1.4 – Test Environment; 6.1 – Tool Support for Testing)*
- Platform: GitHub Actions (simulating minimal deployment hardware)
- Tool: `h1spec` (for RFC compliance and error-handling tests)
- Reporting: GitHub Actions hooks to [Testiny.io](https://www.testiny.io) for test results
- Resource constraints: 20GB disk / 4GB RAM / 1 CPU core

