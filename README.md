# Attacks

## What are the following types of attack?
```
 Man In The Middle (MITM)
 Cross Site Scripting (XSS)
 Cross Site Request Forgery (CSRF)
```
**What is MITM attack**
A man in the middle (MITM) attack is a general term for when a perpetrator positions himself in a conversation between a user and an application—either to eavesdrop or to impersonate one of the parties, making it appear as if a normal exchange of information is underway.

The goal of an attack is to steal personal information, such as login credentials, account details and credit card numbers. Targets are typically the users of financial applications, SaaS businesses, e-commerce sites, and other websites where logging in is required.

![](https://i.imgur.com/52A8v7c.jpg)

**MITM attack progression**
Successful MITM execution has two distinct phases: interception and decryption.

**Interception**
The first step intercepts user traffic through the attacker’s network before it reaches its intended destination.

The most common (and simplest) way of doing this is a passive attack in which an attacker makes free, malicious WiFi hotspots available to the public. Typically named in a way that corresponds to their location, they aren’t password protected. Once a victim connects to such a hotspot, the attacker gains full visibility to any online data exchange.

Attackers wishing to take a more active approach to interception may launch one of the following attacks:

> * IP spoofing
> * ARP spoofing
> * DNS spoofing

**Decryption**
After interception, any two-way SSL traffic needs to be decrypted without alerting the user or application. A number of methods exist to achieve this:

> * HTTPS spoofing
> * SSL BEAST
> * SSL hijacking
> * SSL stripping

### 2. Cross Site Scripting (XSS):-
Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser side script, to a different end user. Flaws that allow these attacks to succeed are quite widespread and occur anywhere a web application uses input from a user within the output it generates without validating or encoding it.

An attacker can use XSS to send a malicious script to an unsuspecting user. The end user’s browser has no way to know that the script should not be trusted, and will execute the script. Because it thinks the script came from a trusted source, the malicious script can access any cookies, session tokens, or other sensitive information retained by the browser and used with that site. These scripts can even rewrite the content of the HTML page.

#### Types of Cross-Site Scripting :-
> * Server XSS

Server XSS occurs when untrusted user supplied data is included in an HTTP response generated by the server. The source of this data could be from the request, or from a stored location. As such, you can have both Reflected Server XSS and Stored Server XSS.

In this case, the entire vulnerability is in server-side code, and the browser is simply rendering the response and executing any valid script embedded in it.

> * Client XSS

Client XSS occurs when untrusted user supplied data is used to update the DOM with an unsafe JavaScript call. A JavaScript call is considered unsafe if it can be used to introduce valid JavaScript into the DOM. This source of this data could be from the DOM, or it could have been sent by the server (via an AJAX call, or a page load). The ultimate source of the data could have been from a request, or from a stored location on the client or the server. As such, you can have both Reflected Client XSS and Stored Client XSS.

With these new definitions, the definition of DOM Based XSS doesn’t change. DOM Based XSS is simply a subset of Client XSS, where the source of the data is somewhere in the DOM, rather than from the Server.

### 3. Cross-Site Request Forgery (CSRF)

CSRF is an attack that tricks the victim into making a malicious request. Inherits the victim's identity and privileges to perform an unwanted function on behalf of the victim, browser requests automatically include any credentials associated with the site, such as user session cookie, IP address, Windows domain credentials, etc. Therefore, if the user is currently authenticated to the site, the site will have no way of distinguishing between the forged request sent by the victim and the legitimate request sent by the victim.

CSRF attacks target functions that change the state on the server, such as changing the victim's email address or password, or buying something. It does no good for the attacker to force the victim to retrieve the data because the attacker does not receive the response, as the victim does. As such, CSRF attacks target state change requests.

#### How does the attack work?
Build a URL or an exploit script
The social engineering side of the attack tricks Alice into bearing this URL when Alice is logged into the bank app. This is usually done with one of the following techniques:
Send unsolicited email containing HTML content
Planting a URL or exploit script on the pages that the victim is likely to visit while they are doing online banking
The exploit URL can be disguised as a normal link, which encourages the victim to click on it

## How can you defend against each of them?

### Man in the middle attack prevention**
> Blocking MITM attacks requires several practical steps on the part of users, as well as a combination of encryption and verification methods for applications.
> For users, this means:
> * Avoiding WiFi connections that aren’t password protected.
> * Paying attention to browser notifications reporting a website as being unsecured.
> * Immediately logging out of a secure application when it’s not in use.
> * Not using public networks (e.g., coffee shops, hotels) when conducting sensitive transactions.

**For website operators :**
> secure communication protocols, including TLS and HTTPS, help mitigate spoofing attacks by robustly encrypting and authenticating transmitted data. Doing so prevents the interception of site traffic and blocks the decryption of sensitive data, such as authentication tokens.
> It is considered best practice for applications to use SSL/TLS to secure every page of their site and not just the pages that require users to log in. Doing so helps decreases the chance of an attacker stealing session cookies from a user browsing on an unsecured section of a website while logged in.

### Cross Site Scripting (XSS)
**Disabling scripts**
> While Web 2.0 and Ajax developers require the use of JavaScript, some web applications are written to allow operation without the need for any client-side scripts. This allows users, if they choose, to disable scripting in their browsers before using the application. In this way, even potentially malicious client-side scripts could be inserted unescaped on a page, and users would not be susceptible to XSS attacks.

**Safely validating untrusted HTML input**

> Many operators of particular web applications (e.g. forums and webmail) allow users to utilize a limited subset of HTML markup. When accepting HTML input from users (say, `<b>very</b>` large), output encoding (such as `&lt;b&gt;very&lt;/b&gt;` large) will not suffice since the user input needs to be rendered as HTML by the browser (so it shows as "`very large`", instead of "`<b>very</b> large`"). Stopping an XSS attack when accepting HTML input from users is much more complex in this situation. Untrusted HTML input must be run through an HTML sanitization engine to ensure that it does not contain XSS code.

### Cross Site Request Forgery (CSRF)

**Synchronizer token pattern**
> Synchronizer token pattern (STP) is a technique where a token, secret and unique value for each request, is embedded by the web application in all HTML forms and verified on the server side. The token may be generated by any method that ensures unpredictability and uniqueness (e.g. using a hash chain of random seed). The attacker is thus unable to place a correct token in their requests to authenticate them.
> 
> Example of STP set by laravel in a HTML form:
> 
`<input type="hidden" name="_token" value="KbyUmhTLMpYj7CD2di7JKP1P3qmLlkPt" />`

**Cookie-to-header token**
Web applications that use JavaScript for the majority of their operations may use the following anti-CSRF technique:

> On an initial visit without an associated server session, the web application sets a cookie which is scoped appropriately so that it should not be provided during cross-origin requests. The cookie typically contains a random token which may remain the same for up to the life of the web session

`Set-Cookie: __Host-csrf_token=i8XNjC4b8KVok4uw5RftR38Wgp2BFwql; Expires=Thu, 23-Jul-2015 10:25:33 GMT; Max-Age=31449600; Path=/; SameSite=Lax; Secure`

> JavaScript operating on the client side reads its value and copies it into a custom HTTP header sent with each transactional request

```
X-Csrf-Token: i8XNjC4b8KVok4uw5RftR38Wgp2BFwql
```

