# Tag JSP

Spring Security fournit des tags permettant d’appliquer des contraintes de sécurité dans une page JSP.

Déclarer la librairie de tag::

```html
<%@ taglib prefix="sec" uri="http://www.springframework.org/security/tags" %>
```

Dépendance Maven::
```xml
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-taglibs</artifactId>
	<version>${spring-security.version}</version>
</dependency>
```

## Tag de contrôle d'accès

```html
<sec:authorize access="hasRole('supervisor')">
    Je ne suis accessible qu'aux utilisateurs ayant le rôle supervisor
</sec:authorize>
<sec:authorize url="/admin">
    Je ne suis accessible qu'aux utilisateurs ayant les droits sur /admin
</sec:authorize>
```
## Tag CSRF Input

```html
   <form method="post" action="/do/something">
       <!-- génération du champ caché CSRF -->
       <sec:csrfInput />
       Name:<br />
       <input type="text" name="name" />
       ...
   </form>
```
## Gérer l'autorisation des URLs

```java
protected void configure(HttpSecurity http) throws Exception {
	http.authorizeRequests()
	        // les requêtes ci-dessous ne seront pas soumises à authentification
			.antMatchers("/resources/**", "/signup", "/about").permitAll()
			// seules les utilisateurs ayant le rôle ADMIN peuvent accéder à /admin
			.antMatchers("/admin/**").hasRole("ADMIN")
			// /db accessible qu'aux ADMIN et DBA
			.antMatchers("/db/**").access("hasRole('ADMIN') and hasRole('DBA')")
			// les autres requêtes sont soumises à authentification
			.anyRequest().authenticated()
			.and()
            // ...
            .formLogin();
}
```