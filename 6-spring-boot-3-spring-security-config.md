# [Importante] Spring Boot 3: Actualización clase SpringSecurityConfig

Actualización para las siguientes clases, usando Spring Boot 3, Spring Security 6 y usando JAVA 17 o 19.

En Spring Security 6, así como otros métodos de configuración para proteger las solicitudes (a saber, y ) se han eliminado de la API. `antMatchers() mvcMathcers() regexMatchers()`

Se introdujo un método sobrecargado `requesMatchers()` como un medio uniforme para asegurar las solicitudes. Los sabores de facilitan todas las formas de restringir las solicitudes que fueron admitidas por los métodos eliminados.

Además, el método `authorizeRequests()` ha quedado obsoleto y ya no debe usarse, ahora en Spring Boot 3 se usa `authorizeHttpRequests()`.

```java
package com.bolsadeideas.springboot.app;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;
     
@Configuration
public class WebSecurityConfig {
        
    @Bean
    public static BCryptPasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
        
    @Bean
    public UserDetailsService userDetailsService()throws Exception{
                    
        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
        manager.createUser(User
               .withUsername("jhon")
               .password(passwordEncoder().encode("12345"))
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
        http
            .authorizeHttpRequests((authz) -> {
                try {
                    authz.requestMatchers("/", "/css/**", "/js/**", "/images/**", "/listar").permitAll()
                        .requestMatchers("/uploads/**").hasAnyRole("USER")
                        .requestMatchers("/ver/**").hasRole("USER")
                        .requestMatchers("/factura/**").hasRole("ADMIN")
                        .requestMatchers("/form/**").hasRole("ADMIN")
                        .requestMatchers("/eliminar/**").hasRole("ADMIN")
                        .anyRequest().authenticated()
                        .and()
                        .formLogin().permitAll()
                        .and()
                        .logout().permitAll();

                } catch (Exception e) {
                        e.printStackTrace();
                }
            });

        return http.build();
            
    }
}
```

Otra forma muy similar para `Spring Boot 3`:

```java
package com.bolsadeideas.springboot.app;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SpringSecurityConfig {


    @Bean
    public static BCryptPasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    public UserDetailsService userDetailsService() throws Exception {

        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();

        manager.createUser(User.withUsername("user")
                               .password(passwordEncoder().encode("user"))
                               .roles("USER").build());

        manager.createUser(User.withUsername("admin")
                               .password(passwordEncoder().encode("admin"))
                               .roles("ADMIN", "USER").build());

        return manager;
    }

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

        http.authorizeHttpRequests(
            (authz) -> authz
                .requestMatchers("/", "/css/**", "/js/**", "/images/**", "/listar").permitAll()
                .requestMatchers("/ver/**").hasAnyRole("USER")
                .requestMatchers("/uploads/**").hasAnyRole("USER")
                .requestMatchers("/form/**").hasAnyRole("ADMIN")
                .requestMatchers("/eliminar/**").hasAnyRole("ADMIN")
                .requestMatchers("/factura/**").hasAnyRole("ADMIN")
                .anyRequest().authenticated()
             )
             .formLogin(login -> login.permitAll())
             .logout(logout -> logout.permitAll());

        return http.build();
    }

}
```

Dejo la documentación oficial de Spring: `Migraciones de configuración :: Spring Security`
https://docs.spring.io/spring-security/reference/5.8/migration/servlet/config.html
