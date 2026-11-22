## Title
Reflected XSS - Cloud Instance Console
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://instance.pwnedbox.site/
The Cloud Instance Console application accepts user input through the fname and lname GET parameters.

During source code analysis, both parameters were found to be processed using PHP's htmlspecialchars() function with the ENT_QUOTES flag.

This function converts special HTML characters and quotes into HTML entities, helping prevent malicious HTML and JavaScript from being executed when the values are displayed in an appropriate HTML context.

Based on the available source code, both parameters have output-encoding protection. No exploitable Reflected XSS vulnerability has been established.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the application: https://instance.pwnedbox.site/

Identify the fname and lname GET parameters.

Provide sample input through the URL parameters.

Observe how the application processes the supplied input.

Inspect the page source or HTTP response.

Verify that special HTML characters are encoded before being reflected in the response.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1018" height="847" alt="image" src="https://github.com/user-attachments/assets/a7b00bb2-01d4-4546-a385-f767fdbeb717" />

<img width="626" height="255" alt="image" src="https://github.com/user-attachments/assets/7abcf41f-8ec9-4058-8188-deaae77685d1" />


<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
No direct Reflected XSS impact can be confirmed from the provided source code.

The use of htmlspecialchars() provides protection against HTML and JavaScript injection through the two examined GET parameters when used in an appropriate output context.

However, other output locations or unsafe JavaScript and DOM operations would require separate investigation.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Continue using htmlspecialchars() with ENT_QUOTES and an explicit UTF-8 encoding.

Apply context-specific output encoding wherever user-controlled data is displayed.

Validate user input according to application requirements.

Avoid directly inserting untrusted input into JavaScript code or HTML attributes.

Review all other user-controlled input sources and output locations for unsafe reflection.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
