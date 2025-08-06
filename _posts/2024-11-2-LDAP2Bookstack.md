---
title: LDAP to BookStack
date: 2024-11-2 4:41:00
categories: [homelab, OAuth]
tags: [homelab]
---

### Introduction  


Before this project I had a grasp of the concept of an IDP but had little knowledge of what went into it's implementation and how it functioned. My main motivation is of course to better understand the technologies that make enterprise environments run, but also because as I am spinning up various containers and making new accounts here and there in my homelab and my Bitwarden is starting to get cluttered. So using an IDP would allow me to consolidate my logins while keeping them secure. Not to mention the convenience of SSO.

Though this is aimed to be educational, it serves equally to reinforce my own learning. If you find something that I can improve upon, please let me know on Linkedin! (Link on main page) So, what is required to run my own IDP for my own applications?...



#### Getting Started

1. What kind of applications are needed? An LDAP Server, IDP, and OAuth2/OIDC compatible web app  
    
    1. Which specific ones? LLDAP, Keycloak, Bookstack in that order
2. How will they be hosted? With Docker of course!

As mentioned in the introduction, OAuth2 and OIDC can provide SSO. This is great because the end user would only need to use one set of credentials to go into applications. Those credentials do have to live somewhere though and although you could maintain all of your user accounts in Keycloak, I find it hard to believe that that is what larger organizations are doing. So where do they keep their users? Likely on a directory server of sorts, whether it be LDAP or Active Directory or another.

As I began to explore my options it was clear that Active Directory was not the best candidate due to it's cost and because of how heavy an AD server would be for my purpose here. After researching, it came down to containers for LLDAP and OpenLDAP. Though OpenLDAP was a more complete solution it was a steeper learning curve and required more time and effort to maintain. LLDAP offers a web GUI and has all of the features that I need for my purposes here.

#### App Layout  

![LDAPtoBSDiagram.png](/assets/LDAPtoBSDiagram.png)


LLDAP is read only from Keycloak currently, though I'll probably change this later. Between LLDAP and Keycloak is LDAPS, which is LDAP over SSL/TLS. By placing a self-signed certificate in the Keycloak trust store I can enable secure communication between these containers. The traffic between Keycloak and BookStack is HTTPS.

The right half of above model consists of the OAuth2/OIDC flow. Understanding the OAuth2 flow types is the second most challenging part to grasp, the first being scopes, claims and mappers. We'll get to that in a moment, first we need to go over the OAuth2 flow. Our specific flow is an "Authorization Flow" because the login process produces an authorization code that the client can use for access and ID tokens.

Really quick... through the following flow you see mentions of front and back channel . A front channel action occurs in "view" of the end user. Front channel actions might carry data through the URL string or via cookies or maybe in headers. Back channel communication occurs independently of the user. "Server" to "server" if you will, without the users involvement.

1. When a user navigates to BookStack they are prompted to login. When they press the login button to initiate a login sequence they are sent to Keycloak. 
    1. Where in keycloak are you redirected? The "Authorization Endpoint"
    2. What does BookStack send front channel with the redirect? Scopes, redirect URI (where should Keycloak send user after auth?), auth type and client ID.
2. Keycloak validates the user through a login process. Mine involves a user/pass and a preconfigured MFA method.
3. After successful validation, Keycloak redirects you back to BookStack with an **authorization code.**
4. BookStack uses this authorization code to exchange for an access token and ID token from Keycloak through a back channel request. The ID token contains information about the user. The access token is used if BookStack needs to make calls back to Keycloak.
    
    1. Included is also the user's group information, you can configure the BookStack roles to map to "External Authentication IDs" which are the groups that exists in LLDAP and Keycloak. (In my case)
5. At the end of you session you can hit the "logout" button. BookStack is configured to use a front channel logout. This means when you click the "Logout" button in BookStack you are redirected to a Keycloak logout endpoint. Your cookies in your browser inform Keycloak of the specific user to logout. This terminates the session within Keycloak and any subsequent site visits will need to go through the login process again.

Here is a diagram to illustrate (Click it to view it closer):

![LDAPBSChart.jpeg](/assets/LDAPBSChart.jpeg)

I know what you are thinking, how do groups work here exactly?

- Well, it starts of course with LLDAP. The groups are synced to Keycloak.
- These groups can have client specific roles assigned to them in the Keycloak group settings.
- Then you'll need to get this group information over to BookStack. This is accomplished through mappers. Mappers control how information is added to a user's token. You can create a "group mapper" to ensure group information is passed into the token. This mapper is included in a scope and maps to a claim.
- A claim is a key-value that provides information in the token. A scope defines what particular information and claims will be included in a token.
- With this configured you just need to specify in the BookStack config the name of the scope to include and the claim to look out for group information.
    
    - I used the following default group config, my additional scope and claim were named "groups" in Keycloak.

This is from the BookStack docs themselves:

![oidcGroupsBookstack.png](/assets/oidcGroupsBookstack.png)

### Final Thoughts

I've omitted most all of the setup details here to highlight the process that occurs instead. For myself, the technical implementation was simple but understanding the mechanics took awhile. There are many great tutorials on each of the components discussed already but the following resources proved to be most helpful during my learning:

- [OktaDev OAuth2/OIDC Introduction](https://www.youtube.com/watch?v=t18YB3xDfXI)
- [LLDAP](https://github.com/lldap/lldap)
- [Keycloak Docs](https://www.keycloak.org/guides)
- BookStack 
    - [Youtube OIDC Tutorial](https://www.youtube.com/watch?v=TJQ4NJrMvkw)
    - [BookStack Docs](https://www.bookstackapp.com/docs/admin/oidc-auth/)
