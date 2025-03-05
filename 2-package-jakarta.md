# Importación de Validaciones en Spring Boot 3 vs Spring Boot 2

Tengan en cuenta para los siguientes videos que en **Spring Boot 3** se cambia `javax` por `jakarta` en la API de validación de Java (**Java API Bean Validation**). 

Por ejemplo, en **Spring Boot 3** se importa de:

```java
import jakarta.validation.Valid;
import jakarta.validation.constraints.NotEmpty;
import jakarta.validation.constraints.Size;
import jakarta.validation.constraints.Email;
import jakarta.validation.constraints.NotNull;
import jakarta.validation.constraints.Pattern;
import jakarta.validation.constraints.Max;
import jakarta.validation.constraints.Min;
```

Y antes, en Spring Boot 2, se importaba de:

```java
import javax.validation.Valid;
import javax.validation.constraints.NotEmpty;
import javax.validation.constraints.Size;
import javax.validation.constraints.Email;
import javax.validation.constraints.NotNull;
import javax.validation.constraints.Pattern;
import javax.validation.constraints.Max;
import javax.validation.constraints.Min;
```

Esto se debe a que Spring Boot 2 usa por debajo (tras bambalinas) en Spring Framework Java EE 8, mientras que Spring Boot 3 usa Jakarta EE 9.
