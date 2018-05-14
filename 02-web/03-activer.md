# Activer Spring Security

Pour configurer Spring Security, créer une classe qui étend `WebSecurityConfigurerAdapter`.

L'annotation `@EnableWebSecurity` active le support de Spring Security dans une application Spring.

```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    
    // rédéfinir des méthodes pour configurer Spring Security
    
}
```