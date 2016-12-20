# WSUDORauth

WSUDORauth is a small, Django application for authenticating users via LDAP.

You can find the GitHub repository here: [https://github.com/WSULib/wsudorauth](https://github.com/WSULib/wsudorauth)

At this time, WSUDORauth is nothing much more than a LDAP login and session manager.  Both Ouroboros and the front-end will ping WSUDORauth and determine if a user's session id in their `WSUDOR` cookie is an active session.

If so, WSUDORauth will return the user's access ID and display names.

WSUDORauth became part of build v2.