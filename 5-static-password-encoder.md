# Actualización siguiente clase: método BCryptPasswordEncoder passwordEncoder()

Un tema que veremos en la siguiente clase sobre el método `passwordEncoder()`. Para evitar un posible error en las ultimas versiones de `spring boot 2.6.0` en adelante:

```BeanCurrentlyInCreationException: Error creating bean with name 'springSecurityConfig': Requested bean is currently in creation: Is there an unresolvable circular reference```

En la clase `SpringSecurityConfig`, tienen que modificar esto por:

```java
	@Bean
	public BCryptPasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder();
	}
```
por 

```java
	@Bean
	public static BCryptPasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder();
	}
```
es decir le agregas la palabra `static`.

Esto es muy importante que lo tengan en cuenta para la siguiente clase (si es que utilizan `Spring Boot 2.6.0 o superior`), agregar el modificador static en el método `passwordEncoder()`
