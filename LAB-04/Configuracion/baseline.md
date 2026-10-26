# **Línea base de seguridad — PostgreSQL 16**

## **1\. Objetivo**

Definir una configuración de referencia para reducir la superficie de ataque de PostgreSQL y proteger las conexiones, los usuarios y los datos.

## **2\. Configuración de red**

| Control | Configuración recomendada |
| ----- | ----- |
| Puerto | `5432`, salvo que exista una justificación para cambiarlo |
| Interfaces de escucha | Solo las interfaces necesarias |
| Firewall | Permitir conexiones únicamente desde redes autorizadas |
| Conexiones remotas | Restringidas a equipos y aplicaciones autorizados |
| `pg_hba.conf` | Reglas específicas para base de datos, usuario, origen y autenticación |

## **3\. Autenticación**

* Preferir `scram-sha-256` cuando los clientes sean compatibles.  
* Evitar reglas de acceso innecesariamente amplias.  
* No compartir contraseñas entre cuentas.  
* Revisar periódicamente las cuentas habilitadas.

## **4\. Roles y privilegios**

* Limitar el uso de `SUPERUSER` a cuentas administrativas autorizadas.  
* Separar las cuentas administrativas de las cuentas de aplicación.  
* Aplicar el principio de mínimo privilegio.  
* Conceder únicamente los permisos necesarios para cada función.

## **5\. Parámetros y conexiones**

Revisar y documentar:

* `max_connections`  
* `superuser_reserved_connections`  
* `statement_timeout`  
* `idle_in_transaction_session_timeout`  
* `log_connections`  
* `log_disconnections`

Los valores deben ajustarse según las necesidades del entorno.

## **6\. Extensiones**

Mantener únicamente las extensiones necesarias para el funcionamiento del sistema. Documentar su propósito y revisar periódicamente su uso.

## **7\. TLS**

* Verificar si SSL/TLS está habilitado.  
* Comprobar si las conexiones utilizan TLS.  
* Utilizar certificados válidos y verificación del servidor cuando corresponda.  
* Evitar transmitir información sensible mediante conexiones sin protección.

## **8\. Sistema operativo**

* Restringir el acceso al directorio de datos y a los archivos de configuración.  
* Permitir su modificación únicamente a cuentas autorizadas.  
* Revisar propietarios, grupos y permisos desde el sistema operativo del servidor.

## **9\. Mantenimiento**

* Aplicar actualizaciones autorizadas.  
* Revisar periódicamente usuarios, permisos y conexiones.  
* Registrar cambios de configuración.  
* Mantener evidencias de las verificaciones realizadas.

## **10\. Estado de la línea base**

Esta línea base representa una propuesta de configuración segura. Su cumplimiento debe verificarse contra la configuración real del servidor antes de declarar los controles como implementados.

