# OWASP TOP 10

## 2017

1. [Injection](#injection)
1. [Broken Authentication and Session Management](#broken-authentication-and-session-management)
1. [Sensitive Data Exposure](#sensitive-data-exposure)
1. [XML External Entities (XXE)[NEW]](#xml-external-entities-(xxe))
1. [Broken Access Control [Merged with 4,7 of OWASP TOP 10-2013]](#broken-access-control)
1. [Security Misconfiguration](#security-misconfiguration)
1. [Cross-Site Scripting (XSS)](#cross-site-scripting-(xss))
1. [Insecure Deserialization[NEW, Community]](#insecure-deserialization)
1. [Using Components with Known Vulnerabilities](#using-components-with-known-vulnerabilities)
1. [Insufficient Logging&Monitoring[NEW, Community]](#insufficient-logging&monitoring)
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

## XML External Entities (XXE)

***Intro:***

    XML is one of the most popular type of file used extensively over the web. XML can include malicious content, External Entities(XML inputs having reference to any local/remote content) which when parsed by XML parsers may disclose sensitive information, execute remote requests and other attacks.

***Reason:***

    1. Most of the old XML parsers allow parsing of external Entities.
    2. The application accepts XML directly even from untrusted sources which when parsed may result in a security breach.
    3. SOAP framework prior to version 1.2 in vulnerable to XXE attack.

***Solution:***

    1. Use less complex data formats such as JSON wherever possible and avoid serikalization of sensitive data.
    2. XML and XSL file upload functionality should validate using XSD.
    3. SAST tools can be used to detect XEE in the source code.
    4. Upgrade all XML processors and libraries in use

***

## Broken Access Control

***Intro:***

    Many times, restrictions on what an authenticated user is allowed to do or authorization is not done before allowing users to use some functions. An attacker may exploit this and gain access to other's accounts, modify data, view sensitive files etc.

***Reason:***

    1. CORS misconfiguration allows unauthorized access of the API.
    2.Access control checks are not properly implemented in restricted functions.

***Solution:***

    1. Deny every other resource by default apart from public resource.
    2. Implement access control mechanisms to authorize user before accessing any protected resource.
    3.JWT tokens should be invalidated on the server after logout.
    4. Ensure that file metadata and backup files are not present within web roots.

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

## Insecure Deserialization

***Intro:***

    To send data(functions/classes/objects etc.) over an HTTP request or store it in the database, we need to convert it into string in an optimized manner. This is knows as Serialisation.
    However, Deserialisation is the opposite i.e converting a string to the original object.
    When an object is made, the default constructor is called therefore, if the serialized string itself have a constructor so upon deserialization it may overload the corrent construction and execute malicious codes.

***Reason:***

    1. Softwares are vulnerable, unsupported or out of date.S
    2. Input validation is not done before Serializing the object.

***Solution:***

    1. Running deserialization in environments with limited permissions.
    2. Keeping a check on deserialization logs and monitoring the failures.
    3. Validate user input.
    4. Accept Serialized strings only from trusted sources

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

## Insufficient Logging&Monitoring

***Intro:***

    Insufficient Logging and Monitoring of data gives the hacker a chance to attack without being detected.

***Reason:***

    1. Events such as logins, falied logins, transactions are not logged.
    2. Logs are not monitored for suspicious activities.
    3. Warnings and errors generate unclear log messages.

***Solution:***

    1. Ensure proper logging of data.
    2. Logs should be monitored for any suspicious attacks.
    3.Ensure logs are generated in a format which can easily be managed by a centralized log management application.

***
***