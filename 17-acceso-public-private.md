# Actualización: Modificadores de acceso en las variables public y private.

Este tutorial es una actualización que hay que tener en cuenta sobre los atributos de la clase componente, cuando tienen que ser `privadas` o `publicas`.

**Atributo Privado:** Ahora en adelante solo hay que usar `private` para atributos que se usan solo dentro de la misma clase componente, pero no fuera de ella, al final es lo mismo que en el lenguaje java donde los atributos `private` solo se acceden dentro de la propia clase.

**Atributo Publico:** Los atributos `public` se se usan dentro y también fuera de la clase componente, por ejemplo en las plantillas html, que acceden a atributos de los componentes, estos atributos deben ser `public` , esto cambio con la última versión de **`TypeScript`**, no tiene relación a angular, sino al lenguaje que usa angular que es **TypeScript**, ahora es más estricto que antes, antes se podía usar `private` también en las vistas html, ahora solo `public`.
