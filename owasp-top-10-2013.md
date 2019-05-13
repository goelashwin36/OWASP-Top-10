# OWASP's TOP 10

## 2013

1. [Injection](#injection)
1. [Broken Authentication and Session Management](#broken-authentication-and-session-management)
1. [Cross-Site Scripting (XSS)](#cross-site-scripting-(xss))
1. [Insecure Direct Object References](#insecure-direct-object-references)
1. [Security Misconfiguration](#security-misconfiguration)
1. [Sensitive Data Exposure](#sensitive-data-exposure)
1. [Missing Function Level Access Control](#missing-function-level-access-control)
1. [Cross-Site Request Forgery (CSRF)](#cross-site-request-forgery-(csrf))
1. [Using Components with Known Vulnerabilities](#using-components-with-known-vulnerabilities)
1. [Unvalidated Redirects and Forwards](#unvalidated-redirects-and-forwards)

***

## Injection

***Intro:***

    In this particular type  of vuln., a malicious code is injected in the input which gets executed in the server side and gives a response. It might lead to severe security breach by disclosing some of the sensitive information unknowingly. Apart from this the server side data may also be modified/deleted or the complete host takeover might also take place.

***Reason:***

    1. Poor data validation.
    2. Directly using input data in queries which might result in execution of complex queries.
    3. Input are directly used in terminals, interpreters.

***Solution:***

    1.Properly validate data before processing.
    2. Use LIMIT and other control statements in SQL to prevent sending large sensitive data.
    3. Use any safe way to execute commands such that input is not directly used in the interpreter/terminal/query.

***

## Broken Authentication and Session Management

***Intro:***

    If the functions in the Application related to authentication and session management are not implemented correctly might lead to a large security breach compromising passwords, session tokens. Sometimes these can be used to access profile of other users and then misuse.

***Reason:***

    1. Session tokens are not random and intead predictable.
    2. Session IDs are exposed in the URL.
    3. Sessions don't timeout.
    4. Session tokens are not check and verified before processing a request.
    5. Proper encryption of passwords, session tokens are not done.

***Solution:***

    1. Session tokens should be randomized.
    2. Proper validation of session tokens should be done before processing a request.
    3. Meet all requirements of OWASP's ASVS areas V2(authentication) and V3(Session Management).

***

## Cross-Site Scripting (XSS)

***Intro:***

    This occurs when data is sent to the browser by the application without any proper validation. It allows the attacker to send payloads which gets executed in the victims browser to hijack user sessions, browser, redirect to malicious urls etc.

    It's of 3 types:
    1. Stores XSS
    2. Reflected XSS
    3. Dom XSS

***Reason:***

    1. No proper validation of the input fields.
    2. Proper output escaping and validation is not done.

***Solution:***

    1. Proper input validation.
    2. Use Content Security Ploicy (CSP) to defend against XSS across your site.
    3. Use auto-sanitization libraries like AntiSamy.
    4. Safe JavaScript APIs must be used. Ajax make it difficult to detect XSS by automated tools.

***

## Insecure Direct Object References

***Intro:***

    IDOR happens when an unauthorized user tries to access restricted resources by changing parameters which point to different objects.

***Reason:***

    1.For direct reference of restricted resources, the used authorization is not checked.
    2. For indirect referecnce of object, the mapping to direct object does not limit the values for those authorized for the current user.

***Solution:***

    1. Instead of using the resource's database id directly, use numbers from '1' to 'n' to display 'n' resources for which the user is authorized and later map this number to the resource's id on the server side.
    2. Before sending an object, an access control check must me done to ensure requested user is authorized.

***

## Security Misconfiguration

***Intro:***

    Due to any minconfiguration at any level be it db services, network, server frameworks, installed services etc. might lead to loss of data, access to protected files/sensitive information, gain unauthirized access etc.

***Reason:***

    1. Not changing default configurations or credentials of various services running.
    2. Security features are not configured properly.
    3. Usage of unnecessary features/services.

***Solution:***

    1. Always change the default credentials/configurations.
    2. Run periodic scans.
    3. Run software updates in a timely manner.

***

## Sensitive Data Exposure

***Intro:***

    It is always possible that some exploit migh lead to disclosure of some of the sensitive information directly as a plain text.

***Reason:***

    1. Sensitive data is stored without encryption.
    2. Old cryptography algorithms are used.
    3. Keys can be easily guessed.

***Solution:***

    1. Always store sensitive data with proper encryption.
    2. Use a strong crypto algorithm with a strong key.
    3. Discard sensitive data asap if not needed.
    4. Passwords must be stored safely using special password protection algorithms.

***

## Missing Function Level Access Control

***Intro:***

    It is possible that an unauthorized user might be able to access some special features simply by accessing the URL etc. For example suppose a feature is hidden for a user in the client side but if any request is sent then it is accepted on the server side.

***Reason:***

    1. Server side authentication/authorisation is not done for restricted functions.
    2. The UI somehow shows navigation to unauthorized functions. Suppose a button is rendered in the frontend but is hidden. If it is made visible then special functions can be executed.

***Solution:***

    1. Deny access to all restricted functions by default and grant permission only upon authorisation.
    2. Find a good way to manage the entitlemets which can be updated and audited easily.

***

## Cross-Site Request Forgery (CSRF)

***Intro:***

    Imagine someone making you send a request to any website unknowingly which can perform harmful actions like making purchase, updating account info, posting on your social media account, logout and even login. This happens when the attacker creates a forged HTTP request and somehow makes you execute it.
    CSRF takes advantage of the fact that the browser sends credentials like session cookies etc. to the server upon sending any request.

***Reason:***

    1. There is no proper verification that the request is legal and is intentionally sent by the user.
    2. Verification of the request is done using HTTP header which does not provide any defense mechanism against CSRF and can be easy modified by the attacker.

***Solution:***

    1. Implement CSRF token(any unique token) which is added in the response body on the first load of the website and every subsequent request should have that same token in the request body.


***

## Using Components with Known Vulnerabilities

***Intro:***

    In our applications we often use components which are vulnerable and can be easily detected by automated scanners and can be exploited.

***Reason:***

    1. Usage of vulnerable components and it's dependencies.
    2. Not updating the components regularly.

***Solution:***

    1. Identify all the components and the verions including their dependencies.
    2. Monitor the security of these components in public databases, security mailing list etc.
    3. Always keep your components up to date.
    4. Wherever possible add security wrappers which disables unused functionality and secures the vulnerable components.
    5. Make security policies about how the components should be used.

***

## Unvalidated Redirects and Forwards

***Intro:***

    Sometimes sites have some links/buttons which redirects to a different page. It can happen in two ways- Indirect and direct redirects. In indirect a parameter is involved which calculated the destination and in direct, the url is opened directly
***Reason:***

    1. The site uses indirect redirects which includes parameters for calculating destination.
    2. Site usually generates redirects(HTTP response codes 300-307, usually 302)

***Solution:***

    1. Avoid using redirects and forwards.
    2. If using redirects then don't use parameters to calculate the destination link. 
    3. If using parameters then verify it in the server using some signature which is part of the parameter.

***
***