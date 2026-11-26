## Title
Stored XSS - Shopify
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://cms.pwnedbox.site/
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the article creation functionality of the CMS application.

The application allows users to submit article content containing HTML elements and JavaScript event handlers without properly sanitizing or encoding the input.

By injecting a malicious HTML payload using an <img> tag with an onerror event handler, JavaScript executes when the published article is rendered.

Since the malicious payload is stored in the application, it continues to execute whenever the affected article content is accessed.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://cms.pwnedbox.site/.

Log in to the application.

Navigate to the Write Article section.

Enter the following XSS payload in the article content or title field:

<img src=x onerror=alert(document.domain)>

Submit and publish the article.

Navigate to the My Articles section.

Open or view the published article.

Observe that a JavaScript alert box appears displaying the domain name cms.pwnedbox.site.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="828" height="627" alt="Screenshot 2026-11-23 060108" src="https://github.com/user-attachments/assets/cd7557f0-e99c-4f03-8743-b83e0d6d5609" />

<img width="1075" height="600" alt="Screenshot 2026-11-23 060128" src="https://github.com/user-attachments/assets/c662ef62-e36a-4270-9ff3-dba79ffa4c28" />

<img width="701" height="831" alt="Screenshot 2026-11-23 061324" src="https://github.com/user-attachments/assets/1c4faea8-1c83-446a-afbb-b16c70799bf5" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could exploit this vulnerability to execute malicious JavaScript in the browser of users viewing the affected article.

Potential consequences include:

Session compromise if sensitive session information is accessible to JavaScript.

Unauthorized actions performed within the victim's authenticated session.

Phishing attacks by displaying fake login forms.

Modification of page content.

Theft of sensitive information accessible through the application's DOM or browser context.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement proper server-side input validation and HTML sanitization.

Encode user-generated content before rendering it in HTML.

Avoid directly inserting untrusted user input into the DOM.

Sanitize permitted HTML using a trusted HTML sanitization library.

Implement a restrictive Content Security Policy (CSP).

Set sensitive session cookies with the HttpOnly, Secure, and appropriate SameSite attributes
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
