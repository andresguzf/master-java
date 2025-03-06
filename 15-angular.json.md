# Actualización: sobre el archivo angular.cli.json vs angular.json

Bueno! esto es un adelanto a las próximas clases, para dejar en claro respecto a los archivos `angular.cli.json` y `angular.json`

## ¿Los archivos angular.cli.json y angular.json son los mismo?

Desde la versión 6 y 7 de angular se pasó a llamar `angular.json`, pero en versiones anteriores de angular se llamaba `angular.cli.json`, pero básicamente son y sirven para lo mismo.

## ¿Por qué no me aparece el angular.cli.json?

Se debe a que estamos trabajando y estamos actualizados a una versión igual o superior a la 7 de angular y en reemplazo tenemos el archivo `angular.json`.

Pero al final y al cabo es exactamente lo mismo, mismo archivo de configuración, mismas configuraciones etc, solo se cambia el nombre y algunos cambios en la estructura del json, pero mínimos.

Por ejemplo, el único detalle que hay que tener presente es que hay que anexar el `src/` en la ruta hacia los recursos o assets js y css. Sería así:
```javascript
    ...
                "styles": [
                  "src/styles.css",
                  "src/assets/css/bootstrap.min.css"
                ],
                "scripts": [
                  "src/assets/js/jquery-3.2.1.slim.min.js",
                  "src/assets/js/popper.min.js",
                  "src/assets/js/bootstrap.min.js"
                ]
    ...
```
