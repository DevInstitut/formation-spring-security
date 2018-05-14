# Sécuriser des méthodes
  
L'annotation  `@EnableGlobalMethodSecurity` active la sécurisation des méthodes via l'utilisation d'annotations.


```java
// la propriété secureEnabled permet d'utiliser l'annotation @Secured
@EnableGlobalMethodSecurity(securedEnabled = true)
public class MethodSecurityConfig {
  // ...
}
```

```java
public interface PizzaService {

  @Secured("IS_AUTHENTICATED_ANONYMOUSLY")
  public Pizza findOnePizza(Long id);

  @Secured("IS_AUTHENTICATED_ANONYMOUSLY")
  public List<Pizza> findAllPizzas();

  // seul les utilisateurs ayant le rôle ADMIN peuvent utiliser cette méthode
  @Secured("ROLE_ADMIN")
  public Pizza create(Pizza account);
}
```