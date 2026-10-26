# **Informe — LAB-04: Hardening y configuración segura de PostgreSQL**

## **1\. ¿Cuál era la principal superficie de ataque?**

La superficie de ataque incluye las conexiones de red, las interfaces de escucha, las reglas de `pg_hba.conf`, las cuentas de usuario y sus privilegios. Estos elementos determinan quién puede intentar acceder al servidor y qué acciones puede realizar.

## **2\. ¿Qué configuración representaba el mayor riesgo?**

Permitir conexiones desde cualquier dirección junto con cuentas que tengan privilegios excesivos representaría un riesgo elevado. Sin embargo, debe verificarse la configuración real antes de afirmar que estas condiciones existen en el servidor.

## **3\. ¿Qué cambio produjo la mayor reducción de exposición?**

Restringir las conexiones a las redes y direcciones necesarias reduciría la exposición del servidor. Esto debe complementarse con reglas específicas en `pg_hba.conf` y permisos mínimos para cada usuario.

## **4\. ¿Qué diferencia existe entre firewall y `pg_hba.conf`?**

El firewall controla qué tráfico de red puede llegar al servidor. `pg_hba.conf` establece qué conexiones de PostgreSQL se permiten según el origen, el usuario, la base de datos y el método de autenticación. Ambos controles trabajan en conjunto.

## **5\. ¿Qué diferencia existe entre autenticación y autorización?**

La autenticación verifica la identidad del usuario que intenta conectarse. La autorización determina qué operaciones puede realizar dentro de la base de datos.

## **6\. ¿Por qué una cuenta de aplicación no debe ser `SUPERUSER`?**

Porque, si la aplicación se compromete, un atacante podría aprovechar todos los privilegios de esa cuenta para afectar otros datos o modificar la configuración. Una cuenta limitada reduce el impacto de un incidente.

## **7\. ¿Por qué cambiar el puerto de PostgreSQL no constituye hardening suficiente?**

Cambiar el puerto predeterminado no impide que un atacante identifique el nuevo puerto. Es necesario aplicar controles de red, autenticación segura y privilegios mínimos.

## **8\. ¿Por qué `listen_addresses='*'` puede ser innecesario?**

Porque configura PostgreSQL para escuchar en todas las interfaces disponibles. Si solo se necesita una interfaz específica, las demás pueden aumentar innecesariamente la exposición.

## **9\. ¿Qué papel tiene el sistema operativo en la seguridad de PostgreSQL?**

El sistema operativo protege los archivos de configuración, las credenciales y el directorio de datos mediante permisos y propietarios. Si una persona no autorizada puede leer o modificar esos archivos, puede comprometer la base de datos incluso cuando los permisos SQL están restringidos.

## **10\. ¿Qué controles deberían revisarse periódicamente?**

Se deben revisar los usuarios y privilegios, las reglas de `pg_hba.conf`, las interfaces de escucha, el firewall, los métodos de autenticación, TLS, las extensiones instaladas, los parámetros de conexión, los permisos del sistema operativo y las actualizaciones.

## **Conclusión**

El hardening de PostgreSQL consiste en reducir los accesos innecesarios, limitar los privilegios y proteger las conexiones y los archivos del sistema. La seguridad debe comprobarse mediante consultas, revisiones de configuración y evidencias, sin asumir que una medida está implementada si todavía no se ha verificado.

