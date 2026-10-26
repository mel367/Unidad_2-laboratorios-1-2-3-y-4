# **Registro de cambios — LAB-04 Hardening**

## **1\. Objetivo**

Documentar las configuraciones revisadas, los riesgos identificados y las mejoras propuestas para PostgreSQL.

## **2\. Registro de revisión**

| Elemento | Estado observado | Acción o propuesta |
| ----- | ----- | ----- |
| Puerto PostgreSQL | Se consultó mediante `SHOW port` | Confirmar que el puerto esté documentado y restringido por red |
| Interfaces de escucha | Se consultó mediante `SHOW listen_addresses` | Verificar que solo se utilicen las interfaces necesarias |
| `pg_hba.conf` | Se consultaron las reglas configuradas | Revisar que las redes y los usuarios estén restringidos |
| Roles | Se consultaron los privilegios mediante `pg_roles` | Limitar los privilegios administrativos |
| Autenticación | Pendiente de confirmar todos los métodos configurados | Preferir `scram-sha-256` cuando sea compatible |
| TLS | Pendiente de completar la verificación | Confirmar el uso de TLS y la configuración de certificados |
| Extensiones | Pendiente de revisión | Identificar extensiones necesarias e innecesarias |
| Parámetros de conexión | Pendiente de completar el registro de valores | Evaluar límites y tiempos de espera |
| Permisos del sistema operativo | No verificados desde el servidor | Solicitar revisión autorizada |
| Firewall | No verificado directamente | Confirmar que solo se permitan orígenes autorizados |

## **3\. Cambios realizados**

Durante la revisión se ejecutaron consultas de inspección para identificar roles y consultar parámetros de configuración.

No se documentan cambios en la configuración global del servidor porque no se ha confirmado que se hayan aplicado modificaciones.

## **4\. Mejoras propuestas**

1. Restringir las interfaces de escucha a las necesarias.  
2. Revisar y limitar las reglas de `pg_hba.conf`.  
3. Separar las cuentas administrativas y de aplicación.  
4. Aplicar el principio de mínimo privilegio.  
5. Verificar el uso de TLS.  
6. Revisar extensiones y parámetros de conexión.  
7. Confirmar la protección de los archivos de configuración y del directorio de datos.  
8. Mantener un registro de cambios y evidencias.

## **5\. Validación**

Antes de considerar implementada una mejora, se debe comprobar el estado posterior al cambio y guardar la evidencia correspondiente.

Las modificaciones que afecten al servidor compartido deben ser autorizadas por su administrador.

## **6\. Conclusión**

La revisión permite identificar controles que deben verificarse para reducir la exposición de PostgreSQL. Las propuestas se documentan como pendientes hasta confirmar su aplicación en el entorno real.

