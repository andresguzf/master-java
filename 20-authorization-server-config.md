# Actualización: Configuración para el servidor de autorización

### AuthorizationServerConfigurerAdapter está deprecated:

Lamentablemente por hoy todavía no se decide que va a pasar con la implementación `AuthorizationServer` en `Spring Security Oauth2`, y es muy probable que no haya nueva implementación para el el servidor de autorización, solo para `Oauth2 Client`, al parecer según lo que se comenta en la comunidad de spring es que solo se va a soportar oauth client, pero pareciera que no el servidor de autorización para generar el token, todavía no hay nada claro, entonces por ahora el equipo de spring recomienda usar versiones anteriores para implementar el servidor de autorización o bien usar algún api externa en la nuve o implementada a mano con jjwt [https://github.com/jwtk/jjwt](https://github.com/jwtk/jjwt).

Por ahora, en el curso utilizar estas versiones:

```xml
		<dependency>
			<groupId>org.springframework.security.oauth</groupId>
			<artifactId>spring-security-oauth2</artifactId>
			<version>2.3.4.RELEASE</version>
		</dependency>
		<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-jwt</artifactId>
			<version>1.0.9.RELEASE</version>
		</dependency>
```
