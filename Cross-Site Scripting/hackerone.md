## Title
Stored XSS - Bug Bounty Platform (HackerOne Clone)
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://hackerone.pwnedbox.site/
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the Bug Bounty Platform's vulnerability report submission functionality.

The application allows users to submit vulnerability reports containing user-controlled input in fields such as Title, Description, and Impact without properly sanitizing or encoding the submitted content.

An attacker can inject malicious JavaScript into these fields. After submitting the report, the application stores the injected content and executes the JavaScript when the report information is displayed on the dashboard or report details page.

This allows malicious scripts to execute in the browser of users viewing the affected report.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://hackerone.pwnedbox.site/.

Navigate to the vulnerability report submission page.

Locate the report submission form.

Enter the following payloads into the respective fields:

Title:

'">shri<script>confirm(1)</script>

Target Program: Select Matomo.

Severity: Select Medium (CVSS 4.0 - 6.9).

Description:

'">shri<script>confirm(2)</script>

Impact:

'">shri<script>confirm(3)</script>

Submit the vulnerability report.

Observe that the application redirects to the dashboard and creates the report (Report ID: #9).

Open or view the submitted report.

Observe that JavaScript confirmation dialogs appear in the browser.

The dialogs displaying 1, 2, and 3 confirm successful JavaScript execution.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1031" height="258" alt="Screenshot 2026-11-23 183338" src="https://github.com/user-attachments/assets/82ea782f-2fe6-4a01-9e5d-2505b0a67dfd" />

<img width="907" height="251" alt="Screenshot 2026-11-23 183344" src="https://github.com/user-attachments/assets/4c4ab3fc-6e10-466a-bfb1-8961260760a5" />

<img width="980" height="407" alt="Screenshot 2026-11-23 183353" src="https://github.com/user-attachments/assets/49b8b405-1cc3-4853-8aa6-2c1248c577aa" />

<img width="1072" height="996" alt="Screenshot 2026-11-23 183441" src="https://github.com/user-attachments/assets/08f36cf8-01a6-42ea-9a38-2b7f41f80bbf" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could exploit this vulnerability to execute arbitrary JavaScript in the browsers of users viewing the affected vulnerability report.

Potential consequences include:

Stealing sensitive information accessible to the application.

Performing unauthorized actions using an authenticated victim's session.

Manipulating vulnerability report content.

Redirecting users to malicious websites.

Conducting phishing attacks against platform users and administrators.

Since the malicious JavaScript is stored in the application, other users viewing the affected report may also be exposed without directly interacting with the attacker.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement proper server-side input validation and sanitization for all report submission fields.

Apply context-aware output encoding before displaying stored user input.

Avoid inserting untrusted input into the DOM using unsafe methods such as innerHTML.

Use safe DOM methods such as textContent when rendering plain text.

Implement a restrictive Content Security Policy (CSP) to mitigate the impact of XSS.

Use a trusted HTML sanitization library if user-submitted HTML is required.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
