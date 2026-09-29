### ¿Qué es una API REST?

Una API REST es una forma de comunicación entre diferentes aplicaciones mediante HTTP, siguiendo un conjunto de reglas basadas en el estilo arquitectónico REST (Representational State Transfer). Su objetivo es permitir que una aplicación pueda solicitar o modificar información que se encuentra en otro sistema. En REST, la información se organiza mediante **recursos**, por ejemplo, usuarios, productos o publicaciones. Cada recurso puede ser identificado mediante una URL. Un **endpoint** es la dirección que permite acceder a un recurso mediante una determinada petición HTTP, por ejemplo, `GET /posts/1` permite solicitar la publicación con el identificador 1. Un ejemplo cotidiano es una aplicación móvil que necesita consultar información de un servidor; mediante una API puede solicitar datos como usuarios, productos, publicaciones o información de una cuenta sin tener acceso directo a la base de datos del servidor.

**Fuentes consultadas:**

* IBM, *What is a REST API?*: https://www.ibm.com/think/topics/rest-apis
* IBM, *Interfaces — RESTful API Design*: https://ibm.github.io/data-science-best-practices/interfaces.html
* MDN Web Docs, *HTTP request methods*: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods
