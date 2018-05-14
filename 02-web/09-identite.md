# Configurer le gestionnaire d'identité

```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
            // l'identité des utilisateurs est stockée en mémoire
            // le préfixe utilisé pour le mot de passe sert à spécifier l'algorithme utilisé
            // {noop} => mot de passe en clair
            auth.inMemoryAuthentication().withUser("root").password("{noop}root").roles("ADMIN");
    }
}
```

## Identité stockée en base de données

Schéma base de données par défaut : voir https://docs.spring.io/spring-security/site/docs/current/reference/html/appendix-schema.html.

```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    @Autowired DataSource dataSource; // bean source de données
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        // l'identité des utilisateurs est stockée en base de données
        auth.jdbcAuthentication()
        .dataSource(dataSource)
        .withDefaultSchema() // cela implique la création de tables users, authorities,...
        .withUser("user").password("password").roles("USER").and()
        .withUser("admin").password("password").roles("USER", "ADMIN");
    }
}
```

## Identité stockée en base de données

```java
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
		auth.jdbcAuthentication() //
			.dataSource(dataSource) // source de données
			.passwordEncoder(passwordEncoder) // choix de l'algorithme d'encodage du mot de passe
			.usersByUsernameQuery("select NOM_UTILISATEUR, MOT_DE_PASSE, EST_ACTIF from UTILISATEUR where NOM_UTILISATEUR=?")
			.authoritiesByUsernameQuery("select NOM_UTILISATEUR,ROLE from UTILISATEUR where NOM_UTILISATEUR = ?");
}
```