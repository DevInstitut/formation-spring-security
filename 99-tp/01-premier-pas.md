# Premiers pas

Premiers pas avec Spring Security

* Ajouter les dépendances suivantes vers _Spring Security Web & Config_ :

```xml
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-web</artifactId>
	<version>4.2.2.RELEASE</version>
</dependency>

<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-config</artifactId>
	<version>4.2.2.RELEASE</version>
</dependency>
```

* Ajouter le filtre Spring Security en créant une classe _dev.paie.web.SecurityWebApplicationInitializer_ :

```java
package dev.paie.web;

import org.springframework.security.web.context.AbstractSecurityWebApplicationInitializer;

public class SecurityWebApplicationInitializer extends AbstractSecurityWebApplicationInitializer{
}
```

* Ajouter la classe de configuration _dev.paie.config.SecurityConfig_ :

```java
package dev.paie.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

	@Override
	protected void configure(AuthenticationManagerBuilder auth) throws Exception {
		auth.inMemoryAuthentication()
			.withUser("admin").password("admin").roles("ADMIN");
	}

	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
		.authorizeRequests().anyRequest().authenticated()
		.and()
		.formLogin();
	}

}
```

* Redémarrer l'application et chercher à accéder à la page http://localhost:8080/paie/mvc/employes/creer. Vous devriez avec l'écran d'authentification suivant :

![](images/login.security.png)

* Connectez-vous et vérifier que l'application fonctionne.
