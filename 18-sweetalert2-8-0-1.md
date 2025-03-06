# Actualización: nueva versión de SweetAlert2 8.0.1 o superior

### Bueno! esto es un adelanto a la próxima clase, para dejar en claro respecto a la última versión del SweetAlert2 (8.x):

Si instalan la última versión del `SweetAlert2`, la `8.10.0` o superior van a obtener un error:

`"Cannot invoke an expression whose type lacks a call signature. "`

Con la nueva versión, solo hay que llamar al método `fire`, según la documentación sería:
```java
        // ES6 Modules or TypeScript
        import swal from 'sweetalert2';
        .... 
        swal.fire(  'The Internet?',  'That thing is still around?',  'success');
        ...
```
[Links: https://sweetalert2.github.io/#examples](https://sweetalert2.github.io/#examples)

Además, en la nueva versión NO agrega automáticamente los estilos CSS, hay que hacerlo a mano en el archivo `angular.json`, por ejemplo agregando los estilos en la propiedad **"styles"**:
```java
                "styles": [
                  "src/styles.css",
                  ...
                  "node_modules/sweetalert2/dist/sweetalert2.min.css",
                ],
```
Otra alternativa, pueden instalar la versión 7.26.9 que usamos en el curso, anterior a la 8:

```
npm install --save sweetalert2@7.26.9
```

Para efectos del curso da lo mismo!
