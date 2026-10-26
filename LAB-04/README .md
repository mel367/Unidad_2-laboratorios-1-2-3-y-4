# **LAB-04 — Hardening y configuración segura de PostgreSQL**

## **Objetivo**

Identificar riesgos en la configuración de PostgreSQL y proponer medidas de hardening para reducir la superficie de ataque, restringir accesos y proteger los datos.

## **Entorno**

* **Sistema:** PostgreSQL 16\.  
* **Herramienta:** pgAdmin 4\.  
* **Puerto predeterminado:** 5432\.  
* **Entorno:** servidor universitario compartido.  
* **Actividades:** revisión de configuración, conexiones, autenticación, roles, privilegios y TLS.

## **Superficie de ataque inicial**

La superficie de ataque incluye el puerto de PostgreSQL, las interfaces de escucha, las conexiones remotas, las reglas de `pg_hba.conf`, los usuarios y sus privilegios, los métodos de autenticación y los archivos de configuración.

## **Hallazgos**

* El rol `postgres` aparece como superusuario.  
* El usuario personal consultado tiene `rolsuper = false` y `rolcreaterole = true`.  
* El rol `analista` tiene privilegios administrativos limitados.  
* Se identificó una membresía del usuario personal en el rol `soporte`.  
* La configuración de red, TLS, firewall y permisos del sistema operativo requiere verificaciones adicionales.

## **Cambios realizados**

Se ejecutaron consultas SQL para inspeccionar roles, privilegios y parámetros de configuración. También se utilizó `GRANT` para conceder membresía en `soporte` y `SET ROLE` para cambiar el rol efectivo de la sesión.

No se han confirmado cambios en la configuración global del servidor. Las medidas adicionales se documentan como propuestas hasta verificar su aplicación.

## **Justificación de los cambios**

La inspección permite conocer los permisos existentes y detectar posibles exposiciones. Las medidas propuestas siguen el principio de mínimo privilegio, restringen las conexiones y promueven el uso de métodos de autenticación seguros.

Las modificaciones globales deben contar con autorización porque el servidor es compartido.

## **Verificación**

Se utilizaron consultas para revisar parámetros como `port`, `listen_addresses`, `ssl` y `password_encryption`, así como información de roles.

También deben verificarse las reglas de `pg_hba.conf`, el uso real de TLS, las extensiones, los permisos del sistema operativo y la exposición de red.

Las verificaciones pendientes no se consideran controles implementados hasta contar con evidencia.

## **Checklist de hardening**

* Inspección de roles y privilegios.  
* Identificación de la membresía en `soporte`.  
* Documentación de riesgos y medidas propuestas.  
* Verificación de interfaces de escucha.  
* Revisión completa de `pg_hba.conf`.  
* Verificación de métodos de autenticación.  
* Comprobación de TLS.  
* Revisión de extensiones.  
* Verificación de permisos del sistema operativo.  
* Revisión del firewall.  
* Comparación de la configuración antes y después.

## **Conclusiones**

El hardening de PostgreSQL requiere controles de red, autenticación, autorización y protección del sistema operativo. Una contraseña fuerte no es suficiente si existen accesos innecesarios o privilegios excesivos.

La práctica permitió revisar roles y documentar medidas de seguridad. Para completar la verificación, deben recopilarse las evidencias de los controles pendientes.

