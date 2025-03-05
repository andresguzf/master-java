# [Importante] Spring Boot 3: Actualización anotación @EnabledMethodSecurity

Actualización para la siguiente clase, usando Spring Boot 3, Spring Security 6 y usando JAVA 17 o 19.
Usar `@EnabledMethodSecurity` en vez de @EnableGlobalMethodSecurity (ya que este se encuentra deprecado) para Spring Boot 3:

```java
@Configuration
@EnableMethodSecurity(securedEnabled = true, prePostEnabled = true)
public class SpringSecurityConfig {

        @Autowired
        private LoginSuccesHandler sucessHandler;

        @Bean 
        public static BCryptPasswordEncoder passwordEncoder() {
            return new BCryptPasswordEncoder();
        }

        @Bean
        public UserDetailsService userDetailsService()throws Exception{
                    
            InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
            manager.createUser(User
                    .withUsername("user")
                    .password(passwordEncoder().encode("user"))
                    .roles("USER")
                    .build());
             manager.createUser(User
                        .withUsername("admin")
                        .password(passwordEncoder().encode("admin"))
                        .roles("ADMIN","USER")
                        .build());
            
            return manager;
        }
        
        @Bean
        public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
     
            http.authorizeRequests().antMatchers("/", "/css/**", "/js/**", "/images/**", "/listar").permitAll()
                    /*.antMatchers("/ver/**").hasAnyRole("USER")*/
                    /*.antMatchers("/uploads/**").hasAnyRole("USER")*/
                    /*.antMatchers("/form/**").hasAnyRole("ADMIN")*/
                    /*.antMatchers("/eliminar/**").hasAnyRole("ADMIN")*/
                    /*.antMatchers("/factura/**").hasAnyRole("ADMIN")*/
                    .anyRequest().authenticated()
                    .and()
                    .formLogin()
                            .successHandler(successHandler)
                            .loginPage("/login")
                        .permitAll()
                    .and()
                    .logout().permitAll()
                    .and()
                    .exceptionHandling().accessDeniedPage("/error_403");
     
            return http.build();
        }
        
}
```
