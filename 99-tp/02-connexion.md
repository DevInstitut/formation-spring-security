# Page de connexion personnalisée

* Compléter la configuration `dev.paie.config.SecurityConfig` comme suit :

```java
...
public class SecurityConfig extends WebSecurityConfigurerAdapter {

	...

	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
		.authorizeRequests().anyRequest().authenticated()
		.and()
		.formLogin()
		.loginPage("/mvc/connexion");
	}

}
```

* Créer un contrôleur pour la page de connexion :

```java
package dev.paie.web.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/connexion")
public class ConnexionController {
	
    // @GetMapping_ est un raccourci pour @RequestMapping(method = RequestMethod.GET)
	@GetMapping
	public String afficherPageCreer() {
		return "connexion";
	}

}
```

* Créer une vue pour la page de connexion `connexion.jsp` :

```html
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Paie - App</title>
		<link rel="stylesheet" href='<c:url value="/bootstrap-3.3.7/css/bootstrap.min.css"></c:url>'>
	</head>
	<body class="container">		

		<h1>Connexion</h1>
		
		<!-- Spring Security s'attend aux paramètres "username" et "password" -->
		<form method="post">
			<input name="username">
			<input name="password">
			<input type="submit" value="Se connecter">
		</form>
		
		<!-- en cas d'erreur un paramètre "error" est créé par Spring Security -->
		<c:if test="${param.error !=null}">
			Erreur d'authentification
		</c:if>
	</body>
</html>
```

* Démarrer l'application et vérifier que c'est désormais une page d'authentification personnalisée.

A ce stade, _Bootstrap_ n'est pas prise en compte. Comprenez-vous pourquoi ?

* Compléter la configuration pour que _Bootstrap_ puisse fonctionner sur cette page.

* Connectez-vous.

A ce stade, l'authentification retourne une erreur :

```
Invalid CSRF Token 'null' was found on the request parameter '_csrf' or header 'X-CSRF-TOKEN'.
```

Pour compléter le Token _CSRF_, nous allons utiliser un _taglib_ Spring Security.

* Ajouter la dépendance suivante :


```xml
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-taglibs</artifactId>
	<version>4.2.2.RELEASE</version>
</dependency>
```

* Compléter la page _connexion.jsp_ comme suit :


```html
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!-- intégration des tags Spring Security -->
<%@ taglib prefix="sec" uri="http://www.springframework.org/security/tags" %>
<!DOCTYPE html>
<html>
	<head>...</head>
	<body class="container">		
		...
		<form method="post">
			<input name="username">
			<input name="password">
			<input type="submit" value="Se connecter">
			
			<!-- génération du Token CSRF -->
			<sec:csrfInput/>
		</form>
		...
	</body>
</html>
```

* Vérifier que la page de connexion fonctionne. Inspectez la page générée pour visualiser le paramètre caché qui manquait.
