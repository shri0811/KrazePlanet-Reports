## Title
Reflected XSS 
**Reflected Cross-Site Scripting (XSS) in the Website Search Box**<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://tutorialrepublic.pwnedbox.site/
The website's search functionality is vulnerable to Reflected Cross-Site Scripting (XSS). User-supplied input entered into the search box is reflected back in the webpage without proper sanitization or context-appropriate output encoding.
An attacker could craft a malicious URL containing JavaScript and trick another user into visiting it. If the injected script executes in the victim's browser, it may allow the attacker to perform actions on behalf of the victim, access sensitive information available to the page, or manipulate webpage content.
This vulnerability occurs because the application does not properly handle untrusted user input before rendering it in the browser!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1.Open the affected website: https://tutorialrepublic.pwnedbox.site/

2.Navigate to the search box on the homepage.

3.Enter the following proof-of-concept payload:
<script>alert(1)</script>

4.Submit the search query.

5.Observe that a JavaScript alert popup displaying 1 appears in the browser.

6.This confirms that the application executes injected JavaScript from the search input, demonstrating Reflected Cross-Site Scripting (XSS).<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1307" height="317" alt="image" src="https://github.com/user-attachments/assets/f80c125c-688d-4b80-b688-79c542126c97" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
The Reflected Cross-Site Scripting (XSS) vulnerability in the website's search functionality could allow an attacker to execute malicious JavaScript in the browser of a victim who interacts with a specially crafted URL.
Successful exploitation may allow an attacker to:

Perform unauthorized actions using the victim's authenticated session, depending on the application's security controls.

Access sensitive information available to JavaScript within the affected page.

Modify webpage content or display misleading information.

Redirect users to malicious websites.

Impersonate the victim within the application's context.

Users who visit a maliciously crafted link may be affected. The actual impact depends on the application's functionality and security controls.!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
1.Input Validation: Validate user-supplied search input and reject unexpected or invalid characters where appropriate.

2.Output Encoding: Apply context-aware HTML encoding to user input before displaying it in the webpage. Characters such as <, >, ", and ' should be safely encoded when rendered as text.

3.Use Safe JavaScript Methods: Avoid inserting untrusted input using dangerous DOM methods such as innerHTML. Prefer safe methods such as textContent.

4.HTML Sanitization: If the application needs to support user-provided HTML, use a maintained HTML sanitization library such as DOMPurify.

5.Content Security Policy (CSP): Implement a properly configured CSP as an additional security layer to restrict unauthorized script execution.

6.Security Testing: Perform regular security assessments to identify and fix XSS vulnerabilities across all user input fields and application endpoints
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
