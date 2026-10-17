

| Situación | Mecanismo apropiado | ¿Qué protege? |
| ----- | ----- | ----- |
| Contraseña de usuario | Hash (`crypt()`)  | Evita guardar la contraseña directamente |
| RFC almacenado en una tabla | Cifrado simétrico  | Protege el RFC y permite recuperarlo con la clave.  |
| Consulta enviada desde un cliente al servidor | TLS  | Protege los datos durante la transmisión.  |
| Respaldo de una base de datos | Cifrado de respaldos  | Evita que otros lean la información del respaldo.  |
| Clave criptográfica | Gestor de secretos  | Evita que la clave quede expuesta o sea usada por personas no autorizadas.  |

