# ✅ Test Plan: RFC9112 §3 Request Line

## 🔹 Test Objective

To verify that the HTTP/1.1 server correctly parses and responds to HTTP request-lines as specified in [RFC9112 §3](https://httpwg.org/specs/rfc9112.html#section-3), including:

* The overall structure: `method SP request-target SP HTTP-version CRLF`
* The correctness and syntax of each individual component:

  * **Method** (§3.1)
  * **Request Target** and its forms (§3.2)
  * **HTTP Version** and line termination (§3.3)

The server must return `400 Bad Request` when encountering malformed syntax, and must respond appropriately to well-formed request-lines.

---

## 🔹 Test Cases

Each test case includes:

* **Test Case ID**
* **Test Description**
* **Preconditions**
* **Test Steps**
* **Expected Result**
* **Actual Result**
* **Status**
* **Comments/Notes**

---

### ✅ TC-RFC9112-3.0-RequestLine-Valid-P0

* **Test Description**: Ensure that the server accepts a syntactically valid request-line.
* **Preconditions**: Server is running and listening on a TCP socket.
* **Test Steps**:

  1. Send: `GET /index.html HTTP/1.1\r\n`
  2. Include a valid `Host` header.
* **Expected Result**: `HTTP/1.1 200 OK` or other valid response.
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Baseline validation for correctly formatted requests.

---

### ❌ TC-RFC9112-3.0-Missing-SP-P0

* **Test Description**: Send a request-line without required space separators.
* **Preconditions**: Server is running and accepts raw TCP input.
* **Test Steps**:

  1. Send: `GET/index.htmlHTTP/1.1\r\n`
* **Expected Result**: `400 Bad Request`
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Validates strict structural compliance.

---

### ❌ TC-RFC9112-3.1-Missing-Method-P0

* **Test Description**: Request-line without an HTTP method.
* **Preconditions**: Server is running.
* **Test Steps**:

  1. Send: ` /index.html HTTP/1.1\r\n`
* **Expected Result**: `400 Bad Request`
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: The method field is mandatory.

---

### ❌ TC-RFC9112-3.1-Unknown-Method-P0

* **Test Description**: Request-line using an undefined method keyword.
* **Preconditions**: Server is running.
* **Test Steps**:

  1. Send: `BOOM /path HTTP/1.1\r\n`
* **Expected Result**: `400 Bad Request` or `501 Not Implemented`
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Syntactically valid but semantically invalid. Behavior may depend on server policy.

---

### ❌ TC-RFC9112-3.2-Missing-Target-P0

* **Test Description**: Missing the request-target field.
* **Preconditions**: Server is running.
* **Test Steps**:

  1. Send: `GET  HTTP/1.1\r\n`
* **Expected Result**: `400 Bad Request`
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Target is required by grammar.

---

### ✅ TC-RFC9112-3.2.1-OriginForm-Valid-P0

* **Test Description**: Valid origin-form request target (`/index.html`).
* **Preconditions**: Server supports path-based routing.
* **Test Steps**:

  1. Send: `GET /index.html HTTP/1.1\r\n`
* **Expected Result**: `HTTP/1.1 200 OK`
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Common use-case.

---

### ✅ TC-RFC9112-3.2.2-AbsoluteForm-Valid-P0

* **Test Description**: Valid absolute-form target for use by proxies.
* **Preconditions**: Proxy handling supported.
* **Test Steps**:

  1. Send: `GET http://example.com/index.html HTTP/1.1\r\n`
* **Expected Result**: Valid response from the proxy (e.g., `200 OK`)
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Used in proxy requests.

---

### ✅ TC-RFC9112-3.2.3-AuthorityForm-Valid-P0

* **Test Description**: Valid authority-form for CONNECT method.
* **Preconditions**: Server supports CONNECT.
* **Test Steps**:

  1. Send: `CONNECT www.example.com:443 HTTP/1.1\r\n`
* **Expected Result**: `200 Connection Established` or `501 Not Implemented`
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Only applicable to CONNECT.

---

### ✅ TC-RFC9112-3.2.4-AsteriskForm-Valid-P0

* **Test Description**: Valid asterisk-form used with OPTIONS.
* **Preconditions**: Server supports OPTIONS.
* **Test Steps**:

  1. Send: `OPTIONS * HTTP/1.1\r\n`
* **Expected Result**: `200 OK` with capabilities
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Used for server-wide capability checks.

---

### ❌ TC-RFC9112-3.3-Missing-CRLF-P0

* **Test Description**: Request-line not terminated with CRLF.
* **Preconditions**: Server allows raw TCP input.
* **Test Steps**:

  1. Send: `GET / HTTP/1.1` (no `\r\n`)
* **Expected Result**: `400 Bad Request` or connection termination
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Validates strict line-ending rule (§3.3)

---

### ❌ TC-RFC9112-3.0-GarbageLine-P0

* **Test Description**: Send invalid non-parsable garbage line.
* **Preconditions**: Server is running.
* **Test Steps**:

  1. Send: `?????\r\n`
* **Expected Result**: `400 Bad Request`
* **Actual Result**: *(To be filled)*
* **Status**: *(Pass / Fail / In Progress)*
* **Comments/Notes**: Ensures robustness against malformed input.

---

## 🔹 Notes

* All test cases are marked as **Priority P0**, as request-line parsing errors pose a protocol compliance risk.
* The test design uses **black-box**, **syntax-based**, and **boundary analysis** techniques, in alignment with **ISTQB Chapter 4**.
* The test plan supports traceability to **RFC9112 §3.x** and can be linked to a Test Management Tool (e.g., Testiny.io).
* Each test case is modular, reusable, and aligned with TransferTask-020 best practices.

