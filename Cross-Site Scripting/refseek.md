## Title
Reflected XSS 
Reflected XSS - RefSeek: Academic & Scientific Search Engine
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://refseek.pwnedbox.site/
The RefSeek website is vulnerable to Reflected Cross-Site Scripting (XSS). The vulnerability occurs when user-supplied input is reflected in the webpage without proper sanitization or context-aware output encoding.

An attacker could craft malicious input containing JavaScript and trick a victim into interacting with it. When the application processes and reflects this input, the injected JavaScript executes in the victim's browser under the website's origin.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open the affected website: https://refseek.pwnedbox.site/
2. Locate the search input field.
3. Enter the following payload:

   `<script>alert(1)</script>`

4. Submit the search query.
5. Observe that a JavaScript alert box displaying `1` appears.
6. Successful execution confirms the Reflected XSS vulnerability.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="970" height="307" alt="image" src="https://github.com/user-attachments/assets/7177c331-4636-4a07-bb67-b4a67c85a117" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Successful exploitation of this vulnerability could allow an attacker to execute arbitrary JavaScript in a victim's browser within the context of the affected website.

Potential consequences include:

- Manipulation of webpage content and appearance.
- Display of misleading or phishing content.
- Execution of unauthorized JavaScript in a victim's browser.
- Access to information exposed to JavaScript on the affected page.
- Potential unauthorized actions within the application's context, depending on the victim's privileges and application security controls.<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
1. **Input Validation:** Validate user-supplied input to ensure it follows the expected format.
2. **Output Encoding:** Apply context-aware output encoding before displaying user-controlled data.
3. **Safe DOM Methods:** Avoid unsafe methods such as `innerHTML`; use `textContent` wherever possible.
4. **HTML Sanitization:** Use trusted sanitization libraries such as DOMPurify if HTML input is required.
5. **Content Security Policy:** Implement a restrictive Content Security Policy (CSP) to reduce the impact of script injection.
6. **Security Testing:** Perform regular security assessments to identify and fix XSS vulnerabilities across the application.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
