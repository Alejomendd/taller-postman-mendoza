### ¿Qué es una API REST?

Una API REST es una forma de comunicación entre diferentes aplicaciones mediante HTTP, siguiendo un conjunto de reglas basadas en el estilo arquitectónico REST (Representational State Transfer). Su objetivo es permitir que una aplicación pueda solicitar o modificar información que se encuentra en otro sistema. En REST, la información se organiza mediante **recursos**, por ejemplo, usuarios, productos o publicaciones. Cada recurso puede ser identificado mediante una URL. Un **endpoint** es la dirección que permite acceder a un recurso mediante una determinada petición HTTP, por ejemplo, `GET /posts/1` permite solicitar la publicación con el identificador 1. Un ejemplo cotidiano es una aplicación móvil que necesita consultar información de un servidor; mediante una API puede solicitar datos como usuarios, productos, publicaciones o información de una cuenta sin tener acceso directo a la base de datos del servidor.

**Fuentes consultadas:**

* IBM, *What is a REST API?*: https://www.ibm.com/think/topics/rest-apis
* IBM, *Interfaces — RESTful API Design*: https://ibm.github.io/data-science-best-practices/interfaces.html
* MDN Web Docs, *HTTP request methods*: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods


## Métodos HTTP

| Método     | Operación CRUD      | ¿Qué hace?                                                                   |
| ---------- | ------------------- | ---------------------------------------------------------------------------- |
| **GET**    | Read (Leer)         | Solicita y obtiene información de uno o varios recursos.                     |
| **POST**   | Create (Crear)      | Envía información al servidor para crear un nuevo recurso.                   |
| **PUT**    | Update (Actualizar) | Reemplaza la información existente de un recurso por la información enviada. |
| **PATCH**  | Update (Actualizar) | Modifica parcialmente un recurso, cambiando solamente los campos necesarios. |
| **DELETE** | Delete (Eliminar)   | Elimina un recurso específico.                                               |

CRUD significa **Create, Read, Update y Delete**, que corresponden a las operaciones básicas para crear, consultar, modificar y eliminar información.


## Códigos de estado

Los códigos de estado HTTP indican qué ocurrió después de realizar una petición al servidor. Se agrupan en cinco familias:

| Familia | Significado                                                                                       | Ejemplo                       |
| ------- | ------------------------------------------------------------------------------------------------- | ----------------------------- |
| **1xx** | Respuestas informativas. Indican que la petición fue recibida y está siendo procesada.            | **100 Continue**              |
| **2xx** | La petición fue procesada correctamente.                                                          | **200 OK**                    |
| **3xx** | Indican redirecciones o que se necesita realizar una acción adicional para completar la petición. | **301 Moved Permanently**     |
| **4xx** | Indican que existe un problema relacionado con la petición realizada por el cliente.              | **404 Not Found**             |
| **5xx** | Indican que ocurrió un problema mientras el servidor intentaba procesar una petición válida.      | **500 Internal Server Error** |

La diferencia principal entre los códigos **4xx y 5xx** está en el origen del problema. Los códigos 4xx normalmente indican que el problema está relacionado con la petición del cliente, por ejemplo, solicitar un recurso que no existe. Los códigos 5xx indican que el servidor encontró un problema al intentar procesar la petición. Por eso, no todos los códigos diferentes de 200 significan que la prueba falló: depende de cuál era el resultado esperado.
