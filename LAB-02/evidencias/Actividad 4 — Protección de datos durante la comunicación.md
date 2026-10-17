**Protección de datos durante la comunicación**

**1\. ¿La conexión actual utiliza TLS?** Depende del resultado de `ssl` en la consulta: `true` significa que sí y `false` que no.

**2\. ¿Qué versión de TLS se está utilizando?** La que aparezca en la columna `version`.

**3\. ¿Qué algoritmo de cifrado aparece?** El que se muestre en la columna `cipher`.

**4\. ¿Qué diferencia existe entre una conexión protegida con TLS y una sin TLS?** Con TLS, los datos viajan cifrados y es más difícil que alguien los lea. Sin TLS, podrían quedar expuestos durante la transmisión.

