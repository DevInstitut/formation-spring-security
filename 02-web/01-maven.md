# Dépendances Maven

Pour utiliser Spring Security dans un contexte Web :

```xml
<dependencies>
   <!-- ... autres dépendances ... -->
   <dependency>
       <groupId>org.springframework.security</groupId>
       <artifactId>spring-security-web</artifactId>
       <version>${spring-security.version}</version>
   </dependency>
   <dependency>
       <groupId>org.springframework.security</groupId>
       <artifactId>spring-security-config</artifactId>
       <version>${spring-security.version}</version>
   </dependency>
</dependencies>
```