## Title
Stored XSS - Events & Polls Activity Center
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://articles.pwnedbox.site/
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the Events & Polls Activity Center, specifically in the Create Community Event functionality.

The application allows users to submit event details such as Event Title, Event Date & Time, and Event Description without properly sanitizing or encoding user-supplied input.

By injecting JavaScript payloads into these fields, an attacker can store malicious scripts in the application. When the saved event information is displayed in the Scheduled Events section, the injected JavaScript executes in the browser.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://articles.pwnedbox.site/.

Navigate to the Events & Polls Activity Center.

Locate the Create Community Event form.

Enter the following payloads into the respective fields:

Event Title:

'">shri<script>confirm(hari)</script>

Event Date & Time:

'">shri<script>confirm(hari1)</script>

Event Description:

'">shri<script>confirm(hari3)</script>

Click the Publish Event button.

Observe the success message indicating that the community event was created successfully.

Check the Scheduled Events section where the submitted event information is displayed.

Observe that the injected JavaScript executes and browser confirmation dialogs appear.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)

<img width="891" height="285" alt="Screenshot 2026-11-23 181454" src="https://github.com/user-attachments/assets/c435ed7f-4c7f-449a-a383-f42c076484c6" />

<img width="1013" height="226" alt="Screenshot 2026-11-23 181502" src="https://github.com/user-attachments/assets/1afaeac5-3dac-48fc-8b85-88940adb282a" />

<img width="972" height="847" alt="Screenshot 2026-11-23 181644" src="https://github.com/user-attachments/assets/f9c40974-54fa-4b5b-83c7-3b5613311910" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could exploit this vulnerability to execute arbitrary JavaScript in the browsers of users viewing the affected event content.

Potential consequences include:

Stealing sensitive information accessible to the application.

Performing unauthorized actions on behalf of authenticated users.

Manipulating page content and user interface elements.

Redirecting users to malicious websites.

Conducting phishing attacks through the trusted application.

Since the payload is stored in the application, multiple users viewing the affected event may be exposed without interacting with the attacker directly.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement proper server-side input validation and sanitization for all event fields.

Apply context-aware output encoding before displaying user-submitted content.

Avoid inserting untrusted user input directly into the DOM using unsafe methods such as innerHTML.

Use safe DOM methods such as textContent when displaying plain text.

Implement a restrictive Content Security Policy (CSP) to reduce the impact of successful XSS attacks.

Use a trusted HTML sanitization library if HTML input is required.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
