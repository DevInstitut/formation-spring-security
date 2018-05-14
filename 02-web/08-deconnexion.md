# Gérer la déconnexion

Si la classe `WebSecurityConfigurerAdapter` est utilisée, la déconnexion est automatiquement configurée.

Une requête `POST /logout` :

* invalide la session
* redirige vers la page d'authentification (_/login?logout_).


##  Personnaliser la déconnexion

Il est possible de personnaliser le comportement de la déconnexion.

```java
protected void configure(HttpSecurity http) throws Exception {
	http.logout()
			.logoutUrl("/autre/logout")
			.logoutSuccessUrl("/autre/index")
			.logoutSuccessHandler(logoutSuccessHandler)
			.invalidateHttpSession(true)
			.addLogoutHandler(logoutHandler)
			.deleteCookies(cookieNamesToClear)
			.and()
		...
}
```