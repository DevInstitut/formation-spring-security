# Spring Security

* Construit sur Spring Framework.
* Fournit plusieurs modèles d’authentification : LDAP, OpenID, Base de données, ...
* Permet de sécuriser une application à plusieurs niveaux : URL, vues, méthode, objet, ...
* Open source.

## Dans quels cas utiliser Spring Security ?
* Une application basée sur la JVM
* Un système d’autorisation/authentification basé sur des rôles.
* Sécuriser une application Web
* S’intégrer avec des systèmes tiers (OpenID, LDAP, Active Directory,
   Base de données,...)
* Sécuriser l’accès à un objet de l’application
* Sécuriser son application de manière déclarative (non intrusif)

## Modules

Spring Security est découpé (depuis la version 3.0) en modules :

* Core (spring-security-core)
* spring-security-cas
* LDAP (spring-security-ldap)
* Config (spring-security-config)
* spring-security-crypto
* Remoting (spring-security-remoting)
* Web (spring-security-web)
* spring-security-acl
* spring-security-taglibs
* spring-security-openid

### Core (spring-security-core)

**Core** contient les classes/interfaces de base pour gérer l'authentification et le contrôle d'accès.
Il est utilisé par tous les autres modules.

Il contient les packages suivants :

* org.springframework.security.core
* org.springframework.security.access
* org.springframework.security.authentication
* org.springframework.security.provisioning

### Remoting (spring-security-remoting)

Intégration avec *Spring Remoting*.

Package de base :

* org.springframework.security.remoting

### Web (spring-security-web)

* Permet d'utiliser Spring Security dans un contexte Web.
* Offre une intégration avec l'API Servlet.

Package de base :

* org.springframework.security.web

### Config (spring-security-config)

* Espaces de nommage utilisés dans la configuration XML
* Classes / Annotations Java utilisées dans la configuration Java

Package de base :

* org.springframework.security.config

### LDAP (spring-security-ldap)

* Authentification LDAP.

Package de base :

* org.springframework.security.ldap

### OAuth 2.0 Core (spring-security-oauth2-core)

* Support de _OAuth 2.0 Authorization Framework_ et _OpenID Connect Core 1.0._

Package de base :

* org.springframework.security.oauth2.core

### OAuth 2.0 Client (spring-security-oauth2-client)

* Support d'un client OAuth 2.0 ou OpenID Connect Core 1.0.

Package de base :

* org.springframework.security.oauth2.client

### OAuth 2.0 JOSE (spring-security-oauth2-jose)

Support de JOSE (Javascript Object Signing and Encryption) construit autour des spécifications suivantes :

* JSON Web Token (JWT)
* JSON Web Signature (JWS)
* JSON Web Encryption (JWE)
* JSON Web Key (JWK)

Package de base :

* org.springframework.security.oauth2.jwt
* org.springframework.security.oauth2.jose

### ACL (spring-security-acl)

Utilisé pour appliquer Spring Security sur des objets métiers.

Package de base :

* org.springframework.security.acls

### CAS (spring-security-cas)

Intégration client CAS (Sigle sign-on).

Package de base :

* org.springframework.security.cas


### OpenID - (spring-security-openid)

* Support de OpenID Web.
* Authentification avec un serveur externe OpenID.
* Requiert OpenID4Java.

Package de base :

* org.springframework.security.openid

### Test - (spring-security-test)

Support des tests Spring Security.
