# Sécurisation par profil

Nous souhaitons désormais autoriser les pages de création uniquement aux administrateurs.

* Compléter la classe _SecurityConfig_ :

```java
@Configuration
@EnableWebSecurity

// Activation de l'utilisation de l'annotation @Secured
@EnableGlobalMethodSecurity(securedEnabled=true) 

public class SecurityConfig extends WebSecurityConfigurerAdapter {

	...
}
```

* Annoter les méthodes des contrôleurs pour gérer les accès. Exemple :

```java

@Controller
@RequestMapping("/employes")
public class RemunerationEmployeController {

	...

	@RequestMapping(method = RequestMethod.GET, path = "/creer")
	@Secured("ROLE_ADMINISTRATEUR")
	public ModelAndView afficherPageCreer() {
		...
	}
	
	@RequestMapping(method = RequestMethod.GET, path = "/lister")
	@Secured({"ROLE_UTILISATEUR", "ROLE_ADMINISTRATEUR"})
	public ModelAndView afficherPageLister(...) {
		...
	}
	
	@RequestMapping(method = RequestMethod.POST, path = "/creer")
	@Secured("ROLE_ADMINISTRATEUR")
	public void creerEmploye(...) {
		...
	}

}
```

* Vérifier l'application de la configuration.   