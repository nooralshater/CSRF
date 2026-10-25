# Exercise 01: Cross-Site Request Forgery (CSRF)

## 1. Vulnerability Description
Cross-Site Request Forgery (CSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they are currently authenticated. With a little help of social engineering (such as sending a link via email or chat), an attacker may trick the users of a web application into executing actions of the attacker's choosing.

A successful CSRF attack can compromise end-user data and operation when targeting a normal user. If the targeted end user is an administrator, a CSRF attack can compromise the entire web application.

According to OWASP, CSRF occurs because web browsers include credentials (such as session cookies, HTTP authentication, or client-side certificates) automatically with every request sent to a specific domain, regardless of which origin generated the request.

## 2. Exploitation Scenarios

### Scenario 1: Hidden Auto-Submitting Form via Phishing Link
An attacker creates a malicious third-party site hosting a hidden HTML form that targets the vulnerable transfer endpoint:
* The victim logs into the banking/transfer application, establishing an active session cookie.
* The victim receives an email or message with a deceptive link leading to the attacker's website.
* Upon loading the page, an automated JavaScript script submits the form immediately in the background without user interaction.
* Because the victim has an active session, the browser automatically includes their session credentials, causing the server to process a $1000 transfer and drain the account to $0.

### Scenario 2: Embedded Cross-Site Resource Injection
An attacker identifies a public platform or web forum where authenticated users gather:
* The attacker embeds a resource payload (such as an `<img>` tag or a malicious script) pointing to the vulnerable transfer action.
* Any active user browsing that forum automatically triggers a GET/POST request to the vulnerable endpoint via their browser.
* The application processes the forged transfer request using the victim's existing session, resulting in unauthorized financial transactions.
