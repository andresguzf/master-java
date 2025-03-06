# [Actualización] modificar el archivo tsconfig.json

Antes de continuar vamos a revisar y modificar el archivo ```tsconfig.json``` que se encuentra en la raíz del proyecto angular, todas las configuraciones que diga `strict` lo cambian a `false`, por ejemplo:

```json
"strict": false,
...
"strictNullChecks": false,
"strictFunctionTypes": false,
"strictBindCallApply": false,
"strictPropertyInitialization": false 
```

etc... y cualquier otra configuración que contenga la palabra strict al comienzo lo cambian a ``false``

Eso es todo, continuemos!
