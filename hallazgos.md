| # | Petición          | Código esperado | Código obtenido | ¿Coincide? |
| - | ----------------- | --------------: | --------------: | ---------- |
| 1 | GET `/posts/1`    |             200 |             200 | Sí         |
| 2 | GET `/posts`      |             200 |             200 | Sí         |
| 3 | GET `/posts/9999` |             404 |             404 | Sí         |
| 4 | POST `/posts`     |             201 |             201 | Sí         |
| 5 | PUT `/posts/1`    |             200 |             200 | Sí         |
| 6 | PATCH `/posts/1`  |             200 |             200 | Sí         |
| 7 | DELETE `/posts/1` |             200 |             200 | Sí         |
