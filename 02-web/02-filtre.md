# `springSecurityFilterChain`

Le filtre `springSecurityFilterChain` :

* protège les ressources Web (URL)
* valide l'authentification
* redirige vers la page d'authentification

La présence dans un projet d'une classe qui étend _AbstractSecurityWebApplicationInitializer_
crée le filtre _springSecurityFilterChain_.

```java
public class SecurityWebApplicationInitializer extends AbstractSecurityWebApplicationInitializer {
}
```