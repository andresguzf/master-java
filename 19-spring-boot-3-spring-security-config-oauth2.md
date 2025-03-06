# [Importante] Spring Boot 3: Actualización clase SpringSecurityConfig

Actualización para las siguientes clases, recomiendo que usen a partir de ahora la versión `2.5.14` de `Spring Boot` para que ademas sea compatible con Spring Security OAuth2, igualmente pueden probar con esta versión de SpringSecurityConfig:
```java
    @EnableMethodSecurity(securedEnabled = true, prePostEnabled = true)
    @Configuration
    public class SpringSecurityConfig {
    
       @Autowired
       private UserDetailsService usuarioService;
     
       @Autowired
       private AuthenticationConfiguration authenticationConfiguration;

       @Bean
       public static BCryptPasswordEncoder passwordEncoder() {
           return new BCryptPasswordEncoder();
       }

       @Bean
       public AuthenticationManager authenticationManager() throws Exception {
           return authenticationConfiguration.getAuthenticationManager();
       }

       @Autowired
       public void userDetailsService(AuthenticationManagerBuilder build) throws Exception {
          build.userDetailsService(usuarioService)
          .passwordEncoder(passwordEncoder());
       }
     
     
       @Bean
       public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
          http.authorizeHttpRequests()
                .anyRequest().authenticated()
                .and()
                .csrf().disable()
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);
          return http.build();
       }
    }
```

### Spring security oauth2 no sea compatible con spring boot 3.

En **Spring Boot 3**, **Spring Security 6** (y usando JAVA 17 o 19), así como otros métodos de configuración para proteger las solicitudes (a saber, y ) se han eliminado de la API. `antMatchers() mvcMathcers() regexMatchers()`

Se introdujo un método sobrecargado `requesMatchers()` como un medio uniforme para asegurar las solicitudes. Los sabores de facilitan todas las formas de restringir las solicitudes que fueron admitidas por los métodos eliminados.

Además, el método `authorizeRequests()` ha quedado obsoleto y ya no debe usarse, ahora en Spring Boot 3 se usa `authorizeHttpRequests()`. 

Pero insisto que es muy probable que Spring OAuth2 no sea compatible con **`Spring Boot 3`** y en ese caso mejor es bajar de versión de **`spring boot 2.5.14`** por mientras ya que todavia se mantiene en paralelo y tiene soporte por el equipo de spring.

[https://spring.io/projects/spring-boot#learn](https://spring.io/projects/spring-boot#learn)

