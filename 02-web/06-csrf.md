# CSRF

CSRF = Cross-Site Request Forgery::
* Type de vulnérabilité des services d’authentification web
* Principe :
** Faire exécuter à un utilisateur une requête HTTP falsifiée qui pointe sur une action interne au site.
* Caractéristiques
** Implique un site qui repose sur l’authentification globale d’un utilisateur
** Exploite cette confiance dans l’authentification pour autoriser des actions implicitement
** Envoie des requêtes HTTP à l’insu de l’utilisateur qui est dupé de déclencher ces actions
* Prévention
** Demander une validation supplémentaire pour les actions critiques (alourdissement du processus ?)
** Utiliser un jeton de validité du formulaire
** Eviter d’utiliser des requêtes GET pour effectuer des modifications du système
** Vérifier le référent (page précédente) dans les pages sensibles

## CSRF activé par défaut

Depuis Spring Security 4.0, par défaut, la protection
CSRF est activée.

Pour désactiver cette protection::

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http.csrf().disable();
}
```

## variable _csrf

Protéger un formulaire via la variable _csrf::

```html
<c:url var="logoutUrl" value="/logout"/>
<form action=“${logoutUrl}" method="post">
    <input type=“submit" value="Log out" />
    <input type=“hidden" name=“${_csrf.parameterName}" value="${_csrf.token}"/>
</form>
```