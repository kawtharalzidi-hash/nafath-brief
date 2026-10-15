Version: NAFATH-V1
Track: Networking

## Overview
This Single Sign-On service lets citizens log in one time to many government services, using a mobile app or a website. Software handles the login: OpenID Connect checks who the user is, and OAuth 2.0 decides what apps can access. Cybersecurity keeps the login safe by using methods like passkeys, so fake websites cannot steal it. Mobile keeps the app limited, so it only asks for things like the camera when it really needs them. AI looks for unusual logins, but it must be fair and private, and people must still review important decisions. Data rules in Oman say what the authority can collect and keep about citizens. All six fields work for one goal, which is that citizens trust the service and their data stay safe. Networking supports this goal through DNS over HTTPS (DoH), which hides DNS requests from people watching the network, but it does not protect everything.

## Software
OAuth 2.0 is built for authorization. It decides what data or resources an app can access, and what permissions it has. It lets an app get limited access using an access token, so the user never has to share their password with it. OpenID Connect is built for authentication. It sits on top of OAuth 2.0 and uses an ID Token to tell the app who the user is. So in our SSO, OIDC handles the user login, and OAuth 2.0 handles delegated access to resources.

Resource: RFC 6749: The OAuth 2.0 Authorization Framework | RFC Editor

## AI
Using the NIST AI Risk Management Framework, the authority must manage these risks before launch. Accuracy and reliability: too many false alarms or missed unusual logins. Bias and fairness: users must be treated fairly. Privacy: protect personal and login data. Security: protect the model from attacks and data manipulation. Transparency: understand why a login is flagged. Accountability: humans can review important decisions. Also keep monitoring after launch.

Resource: AI Risk Management Framework FAQs | NIST

## Mobile
Android keeps every app in its own sandbox, so the login app can’t use sensitive things like the camera, location, or microphone unless the user says yes. The app should ask only when the user starts a feature that needs it, like a QR scan or face scan, not when the app is installed or opened. It should explain why it needs the permission, ask for the minimum only, and still work in a simple way if the user says no.

Resource: Request runtime permissions  |  Privacy  |  Android Developers

## Networking
DNS over HTTPS (DoH) sends DNS requests and answers through an encrypted HTTPS connection. For users of the service, this stops people on the network, like an internet provider, from easily seeing or changing their DNS requests. But it does not protect everything. The DoH provider can still see the requests. It does not encrypt all internet traffic, it does not hide the user’s IP address from websites, and it does not stop phishing or tracking by itself.

Resource: RFC 9076: DNS Privacy Considerations | RFC Editor

## Cybersecurity
A phishing-resistant method stops an attacker from using stolen login information on a fake website, even if the user is tricked into opening it. It works by tying the login to the real website or the secure connection. Methods that qualify are FIDO2/WebAuthn passkeys, FIDO2 security keys, and properly set up PIV/CAC smart cards. Methods that do not qualify are a password with an SMS code, email code, or authenticator-app code, and simple push approval, because an attacker can pass the code on to the real website.

Resource: Authenticators

## Data
Oman’s Personal Data Protection Law (Royal Decree 6/2022) does not directly cover government units. They follow the Personal Data Protection Policy (Circular 6/2024). Because Article 3 has exceptions, the legal team should confirm which rules apply. The authority should collect only needed data, say why it is collected, protect stored data from leaks, and let citizens see and correct their data. It must also follow the rules for storing, sharing, keeping data, and handling breaches.

Resource: Governance - Personal Data Protection | MTCIT

## Misconception in My Track
A common wrong belief is that DNS over HTTPS (DoH) makes the user fully private online, so using it means nobody can see what the user is doing. This is not right. DoH only encrypts the DNS requests, so people on the network, like an internet provider, cannot easily see or change them. But the DoH provider can still see the requests. It also does not encrypt all internet traffic, does not hide the user’s IP address from websites, and does not stop phishing or tracking by itself. The proof is in the RFC 9076 resource, DNS Privacy Considerations, which explains what DoH protects and what it does not.

## Open Question
How can the authority test the AI model and the login methods before launch, so they work correctly, keep citizens' personal information safe, and catch unusual logins without blocking real users?
