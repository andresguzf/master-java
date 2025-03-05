# [Actualización] Para Spring Boot 3: la clase SpringSecurityConfig JWT

Actualización para las siguientes clases, usando `Spring Boot 3`, `Spring Security 6` y usando JAVA 17 o 19.

```java
    package com.bolsadeideas.springboot.app;
     
    import com.bolsadeideas.springboot.app.auth.filter.JWTAuthenticationFilter;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
    import org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration;
    import org.springframework.security.config.annotation.method.configuration.EnableMethodSecurity;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.http.SessionCreationPolicy;
    import org.springframework.security.core.userdetails.UserDetailsService;
    import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
    import org.springframework.security.web.SecurityFilterChain;
    
    import com.bolsadeideas.springboot.app.models.service.JpaUserDetailsService;
     
    @EnableMethodSecurity(securedEnabled = true, prePostEnabled = true)
    @Configuration
    public class SpringSecurityConfig {

       @Autowired
       private BCryptPasswordEncoder passwordEncoder;
     
       @Autowired
       private JpaUserDetailsService userDetailService;
     
       @Autowired
       private AuthenticationConfiguration authenticationConfiguration;
      
       @Bean
       public AuthenticationManager authenticationManager() throws Exception {
           return authenticationConfiguration.getAuthenticationManager();
       }

       @Autowired
       public void userDetailsService(AuthenticationManagerBuilder build) throws Exception {
          build.userDetailsService(userDetailService)
          .passwordEncoder(passwordEncoder);
       }

       @Bean
       public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
          http.authorizeHttpRequests((authz) -> authz
                    .requestMatchers("/", "/css/**", "/js/**", "/images/**", "/listar**","/locale").permitAll()
                    .anyRequest().authenticated()
                )
                .addFilter(new JWTAuthenticationFilter(authenticationManager()))
                .csrf(config -> config.disable())
                .sessionManagement(management -> management.sessionCreationPolicy(SessionCreationPolicy.STATELESS));
          return http.build();
       }
    }

```
