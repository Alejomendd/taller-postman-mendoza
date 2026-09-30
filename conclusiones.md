## 8 - Idempotencia

La idempotencia significa que una operación puede ejecutarse varias veces y el resultado final del recurso no cambia después de la primera ejecución. Es decir, repetir la misma solicitud no debería producir un nuevo cambio en el estado final del recurso.

Para comprobarlo en Postman, ejecuté varias veces la misma petición PUT sobre `/posts/1`, enviando el campo `title` con el valor `"Prueba de idempotencia"`. La respuesta obtenida fue:

```json
{
  "title": "Prueba de idempotencia"
}
```

Al repetir la misma operación, el recurso continuó estableciendo el mismo valor para `title`. Por esta razón, PUT se considera un método idempotente.

También ejecuté varias veces la petición POST sobre `/posts`, utilizando los mismos datos. La respuesta obtenida fue:

```json
{
  "title": "Mi primera prueba",
  "body": "Taller de Ingeniería de Software II",
  "userId": 1,
  "id": 101
}
```

POST se utiliza para solicitar la creación de un recurso. Repetir una solicitud POST puede generar nuevas creaciones, por lo que no se considera un método idempotente.

En conclusión, los métodos GET, PUT y DELETE son idempotentes. POST no es idempotente. PATCH puede ser idempotente o no dependiendo de cómo esté diseñada la operación.

| Método | Idempotente             |
| ------ | ----------------------- |
| GET    | Sí                      |
| POST   | No                      |
| PUT    | Sí                      |
| PATCH  | Depende de la operación |
| DELETE | Sí                      |


## 9 — Las cabeceras de la respuesta

Al revisar las cabeceras de la respuesta de la petición GET `/posts/1`, encontré las siguientes:

| Cabecera      | Valor observado                       | Significado                                                                                                                                           |
| ------------- | ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Content-Type  | `application/json; charset=utf-8`     | Indica el formato de los datos enviados en la respuesta y la codificación utilizada. En este caso, la respuesta está en formato JSON y utiliza UTF-8. |
| Cache-Control | `max-age=43200`                       | Indica durante cuánto tiempo puede considerarse válida una respuesta almacenada en caché. En este caso, son 43.200 segundos, equivalentes a 12 horas. |
| ETag          | `W/"124-yiKdLzqO5gfBrJFrcdJ8Yq0LGnU"` | Es un identificador asociado a una versión del contenido de la respuesta y permite comprobar si el contenido ha cambiado.                             |

La cabecera que considero más importante al probar una API es `Content-Type`, porque permite verificar que el servidor está enviando los datos en el formato esperado. En este caso se esperaba una respuesta JSON y la cabecera confirmó que el contenido recibido tenía ese formato.

Las cabeceras son útiles durante las pruebas porque proporcionan información adicional sobre cómo fue entregada la respuesta, además del código de estado y del contenido del cuerpo.

## 10 — Encuentra el límite

Para encontrar el límite de publicaciones disponibles en la API, realicé pruebas con diferentes valores de ID cercanos al límite.

| ID probado | Código obtenido | Resultado             |
| ---------: | --------------: | --------------------- |
|        100 |          200 OK | Recurso encontrado    |
|        101 |   404 Not Found | Recurso no encontrado |

A partir de estas pruebas se determinó que el **ID más alto que devuelve 200 es 100**, mientras que el **primer ID que devuelve 404 es 101**.

Este tipo de prueba se conoce como **prueba de valores límite**, porque consiste en comprobar los valores que se encuentran en los límites de un rango y los valores inmediatamente fuera de este.

Los defectos pueden concentrarse cerca de los límites porque una aplicación puede manejar correctamente los valores normales, pero presentar errores cuando recibe el último valor permitido o cuando se supera ese límite. Por esta razón, probar tanto el último valor válido como el primero inválido permite comprobar que la aplicación está controlando correctamente sus límites.

## 11 — Explora otros recursos

Se exploraron otros recursos disponibles en JSONPlaceholder diferentes de `/posts`. También se probó una ruta anidada para consultar los comentarios de una publicación específica.

### Recurso `/users`

Se realizó una petición GET a:

`https://jsonplaceholder.typicode.com/users`

La API respondió con el código **200 OK** y devolvió **10 usuarios**.

Cada usuario contiene diferentes campos, entre ellos:

* `id`
* `name`
* `username`
* `email`
* `address`
* `phone`
* `website`
* `company`

Algunos campos, como `address` y `company`, contienen información adicional dentro de objetos.

### Recurso `/todos`

Se realizó una petición GET a:

`https://jsonplaceholder.typicode.com/todos`

La respuesta fue **200 OK** y se obtuvieron **200 elementos**.

Entre los campos observados se encuentran:

* `userId`
* `id`
* `title`
* `completed`

Por ejemplo, el elemento con ID 200 tenía el campo `completed` con el valor `false`.

### Ruta anidada `/posts/1/comments`

Finalmente, se probó la siguiente URL:

`https://jsonplaceholder.typicode.com/posts/1/comments`

La respuesta fue **200 OK** y se obtuvieron **5 comentarios** relacionados con la publicación con ID 1.

Cada comentario contiene campos como:

* `postId`
* `id`
* `name`
* `email`
* `body`

La estructura de la URL se dedujo a partir de la relación entre los recursos. `/posts/1` identifica la publicación con ID 1 y `/comments` permite consultar los comentarios relacionados con esa publicación. Por esto, `/posts/1/comments` puede interpretarse como los comentarios pertenecientes a la publicación 1.

### Resumen

| Petición                | Código | Resultado     |
| ----------------------- | -----: | ------------- |
| GET `/users`            |    200 | 10 usuarios   |
| GET `/todos`            |    200 | 200 tareas    |
| GET `/posts/1/comments` |    200 | 5 comentarios |
