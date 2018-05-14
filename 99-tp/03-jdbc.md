# Authentification via JDBC

## Hashage du mot de passe

* Compléter la classe _dev.paie.config.ServicesConfig_ :

```java
...
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
...
public class ServicesConfig {
	
    // le bean `passwordEncoder` contient l'algorithme de hashage des mots de passe de l'application.
	@Bean
	public PasswordEncoder passwordEncoder() {
	    return new BCryptPasswordEncoder();
	}
	...

}
```

Voici un exemple d'utilisation de ce bean :

```java
@Service
public class InitialiserDonneesServiceDev implements InitialiserDonneesService {

	@Autowired private PasswordEncoder passwordEncoder;

	@Override
	@Transactional
	public void initialiser() {
		String iciUnMotDePasse = "topSecret";
		String iciMotDePasseHashe = this.passwordEncoder.encode(iciUnMotDePasse);
	}

}
```

## Configuration JDBC

L'authentification va être désormais pilotée par une table UTILISATEUR.

* Créer une entité `dev.paie.entite.Utilisateur` :

```java
public class Utilisateur {
	
	public enum ROLES {
		ROLE_ADMINISTRATEUR, ROLE_UTILISATEUR
	}

	private Integer id;
	private String nomUtilisateur;
	private String motDePasse;
	private Boolean estActif;
	private ROLES role;
	...

}
```

* Effectuer le mapping JPA de cette entité.

* Compléter la configuration `dev.paie.config.SecurityConfig` comme suit :

```java
...
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    // injection du bean de hashage de mot de passage
	@Autowired private PasswordEncoder passwordEncoder;
	
	// injection du bean de source de données
	@Autowired private DataSource dataSource;

	@Override
	protected void configure(AuthenticationManagerBuilder auth) throws Exception {
		// changement de stratégie Mémoire => JDBC
	    auth.jdbcAuthentication() 
	        
	        // configuration de la source de données
			.dataSource(dataSource)
			
			// configuration de l'algorithme de hashage des mots de passe
			.passwordEncoder(passwordEncoder)
			
			// requête pour obtenir les informations d'un utilisateur en fonction du nom d'utilisateur
			.usersByUsernameQuery("select NOM_UTILISATEUR, MOT_DE_PASSE, EST_ACTIF from UTILISATEUR where NOM_UTILISATEUR=?") <6>
			
			// requête pour obtenir les rôles d'un utilisateur
			.authoritiesByUsernameQuery("select NOM_UTILISATEUR,ROLE from UTILISATEUR where NOM_UTILISATEUR = ?"); <7>
	}

	...

}

```

* Compléter le service `dev.paie.service.InitialiserDonneesServiceDev` pour insérer des utilisateurs de différents profils au démarrage de l'application.

* Vérifier que l'authentification fonctionne.
