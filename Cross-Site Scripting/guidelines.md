## Title
Reflected XSS - GIGW: Government Website Guidelines Portal
Reflected Cross-Site Scripting (XSS) in the Website Search Functionality
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://guidelines.pwnedbox.site/
The website's search functionality may be vulnerable to Reflected Cross-Site Scripting (XSS). User-supplied input entered through the search box is reflected in the webpage without proper sanitization or context-aware output encoding.
An attacker could potentially craft a malicious URL containing JavaScript and trick a victim into visiting it. If the injected JavaScript executes in the victim's browser, it could allow manipulation of webpage content, access to information available to the page, or unauthorized actions within the application's context.<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open the website: https://guidelines.pwnedbox.site/
2. Locate the search box on the homepage.
3. Enter the following proof-of-concept payload:

   ```html
   <script>alert(1)</script>
   ```
4. Submit the search query.
5. Observe whether a JavaScript alert popup displaying `1` appears.
6. If the alert appears, this demonstrates JavaScript execution through the search functionality.<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="991" height="370" alt="image" src="https://github.com/user-attachments/assets/164075fb-d8fa-4cfc-8c4f-98fbfd54e2dc" />

## Impact
If successfully exploited, this Reflected XSS vulnerability could allow an attacker to execute malicious JavaScript in the browser of a user who visits a specially crafted URL.
Potential consequences include:
Manipulation of webpage content.
Displaying misleading information to website visitors.
Redirecting users to malicious websites.
Accessing sensitive information available to JavaScript within the affected page.
Performing actions on behalf of an authenticated user, depending on application functionality and security controls.
Users who interact with a maliciously crafted link could be affected.<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
1. **Input Validation:** Validate search input and reject unexpected or invalid data where appropriate.
2. **Output Encoding:** Implement context-aware output encoding before displaying user-supplied input in the webpage.
3. **Safe DOM Methods:** Avoid unsafe methods such as `innerHTML` when handling untrusted input. Use `textContent` where appropriate.
4. **HTML Sanitization:** If HTML input is required, use a trusted sanitization library such as DOMPurify.
5. **Content Security Policy (CSP):** Implement a properly configured CSP as an additional layer of protection against script injection.
6. **Security Testing:** Conduct regular security assessments to identify and resolve XSS vulnerabilities in search functionality and other input fields.<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
