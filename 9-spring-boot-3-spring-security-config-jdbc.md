# [Actualización] Para Spring Boot 3: la clase SpringSecurityConfig JDBC

Actualización para la siguiente clase, usando `Spring Boot 3`, `Spring Security 6` y usando JAVA 17 o 19.

```java
@Configuration
@EnableMethodSecurity(securedEnabled = true, prePostEnabled = true)
public class SpringSecurityConfig {
 
    @Autowired
    private LogginSuccessHandler successHandler;
 
    @Autowired
    private BCryptPasswordEncoder passwordEncoder;
 
    @Autowired
    private DataSource dataSource;
 
    @Bean
    SecurityFilterChain filterChain(HttpSecurity http) throws Exception { 
        return http.authorizeHttpRequests(
            (authz) -> authz
                .requestMatchers("/", "/css/**", "/js/**", "/images/**", "/listar")
                .permitAll()
                /*.requestMatchers("/ver/**").hasAnyRole("USER")
                .requestMatchers("/uploads/**").hasAnyRole("USER")
                .requestMatchers("/form/**").hasAnyRole("ADMIN")
                .requestMatchers("/eliminar/**").hasAnyRole("ADMIN")
                .requestMatchers("/factura/**").hasAnyRole("ADMIN")*/
                .anyRequest().authenticated()
             )
             .formLogin(login -> login
                 .successHandler(successHandler)
                 .loginPage("/login")
                 .permitAll())
             .logout(logout -> logout.permitAll())
             .exceptionHandling( ex -> ex.accessDeniedPage("/error_404"))
             .build();
    }
 

    @Bean
    AuthenticationManager authManager(HttpSecurity http) throws Exception {
        return http.getSharedObject(AuthenticationManagerBuilder.class)
                .jdbcAuthentication()
                .dataSource(dataSource)
                .passwordEncoder(passwordEncoder)
                .usersByUsernameQuery("select username, password, enabled from users where username=?")
                .authoritiesByUsernameQuery("select u.username, a.authority from authorities a inner join users u on (a.user_id=u.id) where u.username=?")
                .and().build();
    }
}
  ```
