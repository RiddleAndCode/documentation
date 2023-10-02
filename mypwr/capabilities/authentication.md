# Authentication

For the authentication of the users to the system, a KeyCloak instance is used. Keycloak is an open-source software product to allow single sign-on with Identity and Access Management aimed at modern applications and services.

This authentication service can be provided as a service by Riddle and Code, or it can be hosted by the customer itself. The identities in the backend which are identified only via cryptographic keys, are extended by user specific information like name, email, etc. By this clear separation, user information can stay at the customer or can even be reused from the authentication service of the customer, allowing a better integration into their existing environment and processes.
