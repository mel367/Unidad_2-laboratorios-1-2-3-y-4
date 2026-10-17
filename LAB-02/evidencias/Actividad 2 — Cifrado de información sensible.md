**Cifrado de información sensible**

1\. ¿Qué diferencia existe entre crypt() y pgp\_sym\_encrypt()? 

crypt() sirve para crear un hash de una contraseña, que no se puede recuperar como texto original. En cambio, pgp\_sym\_encrypt() cifra un dato y permite recuperarlo después usando la clave correcta.

2\. ¿Cuál de los dos mecanismos permite recuperar el dato original?

pgp\_sym\_encrypt(), porque se puede descifrar usando la misma clave.

3\. ¿Qué ocurre si se utiliza una clave incorrecta?

PostgreSQL marca un error porque la clave no es la correcta y no puede descifrar el dato.

4\. ¿Qué problema de seguridad representa colocar la clave directamente en una consulta?

Que alguien podría encontrar la clave en el historial o en los registros de las consultas. Si también tiene acceso al dato cifrado, podría descifrarlo y obtener la información original.

