# Actualización: configurando los styles y scripts en archivo angular.json

Esto es un adelanto para la próxima clase, para dejar en claro las diferencias entre los archivos ```angular.cli.json``` y ```angular.json``` respecto a configurar nuestras hojas de estilos **"styles"** y librerías js **"scripts"**.

En las rutas de los **"styles"** y **"scripts"** de  **`../node_modules/`**, debemos que cambiar esto: **`../node_modules/`**  

por esto: ```node_modules/``` (es decir NO hay que incluir el ../ al principio).

 Sería así:
```javascript
    ...
            "styles": [
              "src/styles.css",
              "node_modules/bootstrap/dist/css/bootstrap.min.css"
            ],
            "scripts": [
              "node_modules/jquery/dist/jquery.slim.min.js",
              "node_modules/popper.js/dist/umd/popper.min.js",
              "node_modules/bootstrap/dist/js/bootstrap.min.js"
            ]
    ...

```
