To bypass 2FA, access the subsequent endpoint directly, knowing the path is crucial. If unsuccessful, alter the Referrer header to mimic navigation from the 2FA verification page.
Token Reuse

Reutilizing previously used tokens for authentication within an account can be effective.
Utilization of Unused Tokens

Extracting a token from one's own account to bypass 2FA in another account can be attempted.
Exposure of Token

Investigate whether the token is disclosed in a response from the web application.
Verification Link Exploitation

Using the email verification link sent upon account creation can allow profile access without 2FA, as highlighted in a detailed post.
Session Manipulation

Initiating sessions for both the user's and a victim's account, and completing 2FA for the user's account without proceeding, allows an attempt to access the next step in the victim's account flow, exploiting backend session management limitations.
Password Reset Mechanism

Investigating the password reset function, which logs a user into the application post-reset, for its potential to allow multiple resets using the same link is crucial. Logging in with the newly reset credentials might bypass 2FA.
OAuth Platform Compromise

Compromising a user's account on a trusted OAuth platform (e.g., Google, Facebook) can offer a route to bypass 2FA.
Brute Force Attacks
Rate Limit Absence

The lack of a limit on the number of code attempts allows for brute force attacks, though potential silent rate limiting should be considered.

Note that even if a rate limit is in place you should try to see if the response is different when the valid OTP is sent. In this post, the bug hunter discovered that even if a rate limit is triggered after 20 unsuccessful attempts by responding with 401, if the valid one was sent a 200 response was received.
Slow Brute Force

A slow brute force attack is viable where flow rate limits exist without an overarching rate limit.
Code Resend Limit Reset

Resending the code resets the rate limit, facilitating continued brute force attempts.
Client-Side Rate Limit Circumvention

A document details techniques for bypassing client-side rate limiting.
Internal Actions Lack Rate Limit

Rate limits may protect login attempts but not internal account actions.
SMS Code Resend Costs

Excessive resending of codes via SMS incurs costs to the company, though it does not bypass 2FA.
Infinite OTP Regeneration

Endless OTP generation with simple codes allows brute force by retrying a small set of codes.
Race Condition Exploitation

Exploiting race conditions for 2FA bypass can be found in a specific document.
CSRF/Clickjacking Vulnerabilities

Exploring CSRF or Clickjacking vulnerabilities to disable 2FA is a viable strategy.
"Remember Me" Feature Exploits
Predictable Cookie Values

Guessing the "remember me" cookie value can bypass restrictions.
IP Address Impersonation

Impersonating the victim's IP address through the X-Forwarded-For header can bypass restrictions.
Utilizing Older Versions
Subdomains

Testing subdomains may use outdated versions lacking 2FA support or contain vulnerable 2FA implementations.
API Endpoints

Older API versions, indicated by /v*/ directory paths, may be vulnerable to 2FA bypass methods.
Handling of Previous Sessions

Terminating existing sessions upon 2FA activation secures accounts against unauthorized access from compromised sessions.
Access Control Flaws with Backup Codes

Immediate generation and potential unauthorized retrieval of backup codes upon 2FA activation, especially with CORS misconfigurations/XSS vulnerabilities, poses a risk.
Information Disclosure on 2FA Page

Sensitive information disclosure (e.g., phone number) on the 2FA verification page is a concern.
Password Reset Disabling 2FA

A process demonstrating a potential bypass method involves account creation, 2FA activation, password reset, and subsequent login without the 2FA requirement.
Decoy Requests

Utilizing decoy requests to obfuscate brute force attempts or mislead rate limiting mechanisms adds another layer to bypass strategies. Crafting such requests requires a nuanced understanding of the application's security measures and rate limiting behaviours.
OTP Construction errors

In case the OTP is created based on data the user already has or that is sending previous to create the OTP, it's possible for the user to also generate it and bypass it.
References

    https://medium.com/@iSecMax/two-factor-authentication-security-testing-and-possible-bypasses-f65650412b35
    https://azwi.medium.com/2-factor-authentication-bypass-3b2bbd907718
    https://getpocket.com/read/aM7dap2bTo21bg6fRDAV2c5thng5T48b3f0Pd1geW2u186eafibdXj7aA78Ip116_1d0f6ce59992222b0812b7cab19a4bce