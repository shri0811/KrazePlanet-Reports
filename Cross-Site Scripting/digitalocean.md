## Title
Stored XSS - Support Center (DigitalOcean Clone)
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://digitalocean.pwnedbox.site/
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the Support Center's Support Tickets functionality.

The application allows user-controlled input to be submitted and stored as support ticket information without properly sanitizing or encoding the input.

An attacker can inject malicious JavaScript into ticket-related fields. Once the ticket is submitted and displayed in the Open Tickets section, the injected JavaScript executes in the browser.

This demonstrates that the application does not properly handle untrusted user input before rendering stored ticket information.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://digitalocean.pwnedbox.site/.

Navigate to the Support Center.

Open the Support Tickets section.

Locate the support ticket submission functionality.

Enter the following test payload into a user-controlled ticket field:

'">shri<script>confirm(1)</script>

Submit the support ticket.

Navigate to the Open Tickets section.

Observe that the submitted ticket information is displayed.

Observe the JavaScript confirmation dialogs appearing in the browser.

The successful execution confirms the Stored XSS vulnerability.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)

<img width="985" height="312" alt="Screenshot 2026-11-23 182745" src="https://github.com/user-attachments/assets/869f1a9c-802a-4d94-9b0d-58ea7a185de2" />
<img width="967" height="300" alt="Screenshot 2026-11-23 182752" src="https://github.com/user-attachments/assets/2127c844-f28e-46d9-a751-eae2cc44fb75" />
<img width="1522" height="892" alt="Screenshot 2026-11-23 182808" src="https://github.com/user-attachments/assets/9bea2049-6d0d-4a7a-8864-4a6e53c0f1eb" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could exploit this vulnerability to execute arbitrary JavaScript in the browsers of users viewing the affected support tickets.

Potential impacts include:

Stealing sensitive information accessible to the application.

Performing unauthorized actions using an authenticated victim's session.

Manipulating displayed ticket information.

Redirecting users to malicious websites.

Conducting phishing attacks against support staff and other users.

Since the malicious payload is stored, other users accessing the affected ticket information may also become victims without directly interacting with the attacker.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement server-side input validation and sanitization for all support ticket fields.

Apply context-aware output encoding before displaying stored user input.

Avoid rendering untrusted data using unsafe DOM methods such as innerHTML.

Use safe DOM properties such as textContent for displaying plain text.

Implement a restrictive Content Security Policy (CSP) to reduce the impact of XSS.

Use a trusted HTML sanitization library wherever user-submitted HTML is required.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
