# Configuration Http

```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        
        // toutes les requêtes doivent être authentifiées
    	http.authorizeRequests().anyRequest().authenticated()
    	
    	        // Permettre  aux utilisateurs de s'authentifier via une page d'authentification
    			.and().formLogin()
    			
    			// Permettre aux utilisateurs de s'authentifier via HTTP Basic Authentification
    			.and().httpBasic();
    }
    
}
```