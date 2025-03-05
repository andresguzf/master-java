# [Importante] Update Spring Boot 3: dependencia thymeleaf-extras-springsecurity6

Un tema que veremos en la siguiente clase sobre las dependencias del pom.xml de Spring Security. 

Para los que vengan utilizando el **Spring Boot 3** o superior la dependencia **Thymeleaf Extras Security 5** no es compatible con **Spring Security 6**. Por lo tanto, debemos de agregar la siguiente dependencia en el `pom.xml`, a partir de la versión de Spring Boot 3, nos obliga a colocar la versión de esta dependencia.

Entonces la versión de Spring Boot 3 en adelante la dependencia `thymeleaf-extras-springsecurity6` debe quedar:

```XML
    <dependency>
      <groupId>org.thymeleaf.extras</groupId>
      <artifactId>thymeleaf-extras-springsecurity6</artifactId>
    </dependency>
```
Es decir es la versión 6 en vez de la 5, entonces para Spring Boot 3 es `thymeleaf-extras-springsecurity6` y en versiones de Spring Boot 2 es `thymeleaf-extras-springsecurity5`
