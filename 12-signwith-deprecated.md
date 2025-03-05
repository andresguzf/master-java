# Actualización: SignWith deprecated utilizando últimas versiones de jjwt

Bueno! esto es un adelanto a la próxima clase, para dejar en claro respecto a las últimas versiones de **io.jsonwebtoken (jjwt)**:

Si instalan la última versión del **io.jsonwebtoken**, la `0.10.5` o superior van a obtener un warning: `"signWith is deprecated"`

Cambió un poco, en ese caso  tienes que usar la llave secreta de forma automática, básicamente debería ser así:
```java
            SecretKey secretKey = Keys.secretKeyFor(SignatureAlgorithm.HS512);
            		
            String token = Jwts.builder()
                            .setSubject(username)
                            .signWith(secretKey)
                            .compact();
```

Hay diferentes formas, la idea es inicializarlo una sola vez, por ejemplo puede ser en una constante de la clase:
```java
public static final Key SECRET_KEY = Keys.secretKeyFor(SignatureAlgorithm.HS512);
```

Luego ocupas la constante tanto para generar el token con signWith(SECRET_KEY) como para validarlo con setSigningKey(SECRET_KEY):

Generar:
```java
        String token = Jwts.builder()
            .setClaims(claims)
            .setSubject(username)
            .signWith(SECRET_KEY)
            .setExpiration(new Date(System.currentTimeMillis() + 3600000*4)).compact();
```

Validar:
```java
            try {
                 Claims claims = Jwts.parser()
                .setSigningKey(SECRET_KEY)
                .parseClaimsJws(resolve(token)).getBody();
            } catch (JwtException | IllegalArgumentException e) ...
```

También puedes implementar una clave secreta pero de forma estática, es decir que uno mismo le asigne el valor, y no que se genere de forma automática, para eso puedes usar el método hmacShaKeyFor(byte[] bytes), por ejemplo:

`SecretKey secretKey = Keys.hmacShaKeyFor("algunaLlaveSecreta".getBytes())`

O bien crear una instancia de la clase SecretKeySpec con el operador new para generar el SecretKey:

`SecretKey secretKey = new SecretKeySpec("algunaLlaveSecreta".getBytes(), SignatureAlgorithm.HS256.getJcaName());`

### De dependencias `pom.xml`:

Ahora en las últimas versiones`0.10.5` o superior son 3:

```XML
		<!-- jjwt -->
		<dependency>
			<groupId>io.jsonwebtoken</groupId>
			<artifactId>jjwt-api</artifactId>
			<version>0.10.5</version>
		</dependency>
		<dependency>
			<groupId>io.jsonwebtoken</groupId>
			<artifactId>jjwt-impl</artifactId>
			<version>0.10.5</version>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>io.jsonwebtoken</groupId>
			<artifactId>jjwt-jackson</artifactId>
			<version>0.10.5</version>
			<scope>runtime</scope>
		</dependency>
```
