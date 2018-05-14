# Personnaliser la page d'authentification

```java
protected void configure(HttpSecurity http) throws Exception {
	http
		.authorizeRequests()
			.anyRequest().authenticated()
			.and()
		.formLogin()
			.loginPage("/login")
			.permitAll(); // ne pas soumettre à l'authentification, la page de connexion
}
```

## Exemple de page d'authentification

```html
<c:url value="/login" var="loginUrl"/>
<form action="${loginUrl}" method="post">
	<c:if test="${param.error != null}">
		<p>Invalid username and password.</p>
	</c:if>
	<c:if test="${param.logout != null}">
		<p>You have been logged out.</p>
	</c:if>
	<p>
		<label for="username">Username</label>
		<input type="text" id="username" name="username"/>
	</p>
	<p>
		<label for="password">Password</label>
		<input type="password" id="password" name="password"/>
	</p>
	<input type="hidden" name="${_csrf.parameterName}" value="${_csrf.token}"/>
	<button type="submit" class="btn">Log in</button>
</form>
```