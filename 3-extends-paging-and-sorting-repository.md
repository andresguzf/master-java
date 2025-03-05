# Actualización: para Spring Boot 3 o superior para PagingAndSortingRepository

Tengan en cuenta para los siguientes videos que en **Spring Boot 3** la interface `PagingAndSortingRepository` ya no extiende de `CrudRepository` sino que extiende de `Repository` y no incluye los métodos del **Crud**.

Tenemos dos soluciones:

**La primera** es en vez de usar `PagingAndSortingRepository` extendemos de `JpaRepository`:

```java
public interface IClienteDao extends JpaRepository<Cliente, Long>{
}
```

**La segunda solución** es extender de ambas separado por coma, de `PagingAndSortingRepository` y `CrudRepository`:

```java
public interface IClienteDao extends PagingAndSortingRepository<Cliente, Long>, CrudRepository<Cliente, Long>{
}
```
