# Hallazgos

## Tabla de peticiones de la Fase 2

| # | Petición          | Código esperado | Código obtenido | ¿Coincide? |
| - | ----------------- | --------------: | --------------: | ---------- |
| 1 | GET `/posts/1`    |             200 |             200 | Sí         |
| 2 | GET `/posts`      |             200 |             200 | Sí         |
| 3 | GET `/posts/9999` |             404 |             404 | Sí         |
| 4 | POST `/posts`     |             201 |             201 | Sí         |
| 5 | PUT `/posts/1`    |             200 |             200 | Sí         |
| 6 | PATCH `/posts/1`  |             200 |             200 | Sí         |
| 7 | DELETE `/posts/1` |             200 |             200 | Sí         |

---

# Tarea 4 — Lee un recurso y la colección completa

## GET `/posts/1`

Se realizó una petición GET al recurso:

`https://jsonplaceholder.typicode.com/posts/1`

La respuesta obtenida fue **200 OK**.

La respuesta corresponde a un solo recurso y contiene los siguientes campos:

* `userId`
* `id`
* `title`
* `body`

Por lo tanto, al solicitar un recurso específico se espera recibir un solo elemento con la información correspondiente a ese recurso.

## GET `/posts`

Se realizó una petición GET a:

`https://jsonplaceholder.typicode.com/posts`

La respuesta obtenida fue **200 OK** y se recibieron **100 publicaciones**.

Cada publicación contiene los campos:

* `userId`
* `id`
* `title`
* `body`

## Diferencia en los criterios de aceptación

Cuando se solicita un recurso específico, se debe comprobar que el recurso solicitado exista, que tenga el identificador correcto y que sus campos esperados estén presentes.

Cuando se solicita una colección, además de comprobar que la respuesta sea correcta, se debe verificar que se reciba una lista de elementos y que cada elemento tenga la estructura esperada.

Por esta razón, los criterios de aceptación cambian dependiendo de si se está comprobando un recurso individual o una colección.

---

# Tarea 5 — Provoca un error a propósito

Se realizó la petición:

`GET https://jsonplaceholder.typicode.com/posts/9999`

Antes de ejecutarla se esperaba obtener un código **404 Not Found**, debido a que se estaba solicitando un recurso que no existe.

El código obtenido fue:

**404 Not Found**

El caso de prueba **pasó**, porque el resultado obtenido coincidió con el resultado esperado. Un código 404 no significa automáticamente que una prueba haya fallado. En este caso, era precisamente la respuesta que se esperaba obtener.

Si la misma petición hubiera devuelto un código **200 OK** con un cuerpo vacío, se consideraría un defecto en relación con este caso de prueba, porque el resultado obtenido sería diferente al resultado esperado. La prueba busca comprobar que un recurso inexistente sea identificado correctamente.

---

# Tarea 6 — Crea un recurso con POST

Para realizar la prueba se utilizó el método POST sobre:

`https://jsonplaceholder.typicode.com/posts`

Se envió el siguiente contenido en formato JSON:

```json
{
  "title": "Mi primera prueba",
  "body": "Taller de Ingeniería de Software II",
  "userId": 1
}
```

La petición devolvió un código **201 Created** y una respuesta similar a:

```json
{
  "title": "Mi primera prueba",
  "body": "Taller de Ingeniería de Software II",
  "userId": 1,
  "id": 101
}
```

La petición se ejecutó varias veces y se observó que JSONPlaceholder responde simulando la creación del recurso. El identificador devuelto permite observar el resultado de la operación.

Esto ocurre porque JSONPlaceholder es una API de prueba que simula operaciones de creación, modificación y eliminación, por lo que las operaciones no deben interpretarse como cambios permanentes en una base de datos real.

En una API real, para comprobar que un recurso fue creado realmente, se podría consultar posteriormente el recurso mediante una petición GET utilizando el identificador obtenido, o verificar directamente en la base de datos o mediante otro mecanismo de confirmación proporcionado por la API.

---

# Tarea 7 — Diferencia entre PUT y PATCH

Para comparar ambos métodos se utilizaron las peticiones:

* `PUT /posts/1`
* `PATCH /posts/1`

En ambas se envió únicamente el campo `title`.

## PUT

Se utilizó el siguiente contenido:

```json
{
  "title": "Prueba de idempotencia"
}
```

La respuesta observada fue:

```json
{
  "title": "Prueba de idempotencia"
}
```

El código de respuesta fue **200 OK**.

## PATCH

Para PATCH se utilizó el mismo campo:

```json
{
  "title": "Prueba de idempotencia"
}
```

La respuesta fue **200 OK**.

## Diferencia encontrada

PUT se utiliza normalmente para reemplazar o establecer la representación de un recurso completo, mientras que PATCH está pensado para realizar una modificación parcial.

Aunque en esta prueba ambos métodos recibieron solamente el campo `title`, la diferencia principal está en la intención de cada método. PATCH permite indicar que solamente se desea modificar una parte del recurso.

Para corregir un error de escritura en un solo campo utilizaría **PATCH**, porque la operación consiste en modificar únicamente ese campo sin tener que plantear el cambio como un reemplazo completo del recurso.

---

# Tarea 10 — Encuentra el límite

Para encontrar el límite de publicaciones disponibles se realizaron pruebas con identificadores cercanos al límite.

| ID probado | Código obtenido | Resultado             |
| ---------: | --------------: | --------------------- |
|        100 |          200 OK | Recurso encontrado    |
|        101 |   404 Not Found | Recurso no encontrado |

A partir de estas pruebas se determinó que el **ID más alto que devuelve 200 es 100**, mientras que el **primer ID que devuelve 404 es 101**.

Este tipo de prueba se conoce como **prueba de valores límite**, porque consiste en comprobar los valores que se encuentran en los límites de un rango y los valores inmediatamente fuera de este.

Los defectos pueden concentrarse cerca de los límites porque una aplicación puede funcionar correctamente con valores normales, pero presentar problemas al recibir el último valor permitido o al superar dicho límite. Por esta razón, resulta importante probar tanto el último valor válido como el primero inválido.

---

# Tarea 11 — Explora otros recursos

Se exploraron otros recursos disponibles en JSONPlaceholder diferentes de `/posts`. También se probó una ruta anidada para consultar los comentarios de una publicación específica.

## Recurso `/users`

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

## Recurso `/todos`

Se realizó una petición GET a:

`https://jsonplaceholder.typicode.com/todos`

La respuesta fue **200 OK** y se obtuvieron **200 elementos**.

Entre los campos observados se encuentran:

* `userId`
* `id`
* `title`
* `completed`

Por ejemplo, el elemento con ID 200 tenía el campo `completed` con el valor `false`.

## Ruta anidada `/posts/1/comments`

Se probó la siguiente URL:

`https://jsonplaceholder.typicode.com/posts/1/comments`

La respuesta fue **200 OK** y se obtuvieron **5 comentarios** relacionados con la publicación con ID 1.

Cada comentario contiene campos como:

* `postId`
* `id`
* `name`
* `email`
* `body`

La estructura de la URL se dedujo a partir de la relación entre los recursos. `/posts/1` identifica la publicación con ID 1 y `/comments` permite consultar los comentarios relacionados con esa publicación.

Por esta razón, `/posts/1/comments` puede interpretarse como los comentarios pertenecientes a la publicación con ID 1.

---

# Tarea 13 — Pruebas automáticas propias

Además de la prueba que verifica el código de estado, se crearon tres pruebas adicionales sobre la petición GET `/posts/1`.

## Prueba 1 — Existencia del campo `title`

```javascript
pm.test("La respuesta contiene el campo title", function () {
    pm.expect(pm.response.json()).to.have.property("title");
});
```

Esta prueba verifica que la respuesta contenga un campo llamado `title`.

## Prueba 2 — Valor del campo `id`

```javascript
pm.test("El ID del recurso es 1", function () {
    pm.expect(pm.response.json().id).to.eql(1);
});
```

Esta prueba comprueba que el valor del campo `id` sea exactamente `1`, debido a que la petición corresponde al recurso `/posts/1`.

## Prueba 3 — Tipo de dato de `userId`

```javascript
pm.test("El campo userId es un número", function () {
    pm.expect(pm.response.json().userId).to.be.a("number");
});
```

Esta prueba verifica que el campo `userId` sea de tipo numérico.

Las tres pruebas adicionales se ejecutaron correctamente y aparecieron en verde. Junto con la prueba del código de estado realizada en la Tarea 12, se tienen cuatro verificaciones automáticas diferentes para la respuesta de la API.
