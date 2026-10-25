# **Privacidad y protección de datos en bases de datos**

## **1\. Introducción**

En esta práctica se analizaron los problemas de privacidad que pueden presentarse al almacenar información de clientes. Tener una base de datos segura no solo consiste en configurar usuarios y contraseñas, también es necesario definir para qué se utilizan los datos, quién puede consultarlos y cuánto tiempo deben conservarse.

## **2\. Inventario de datos**

| Dato | Clasificación | Protección necesaria |
| ----- | ----- | ----- |
| ID | Identificador del registro | Control de acceso |
| Nombre | Dato personal | Acceso restringido |
| Correo | Dato personal | Acceso restringido y enmascaramiento |
| Teléfono | Dato personal | Acceso restringido y enmascaramiento |
| RFC | Dato personal de identificación fiscal | Cifrado y acceso limitado |
| Edad | Dato personal | Uso limitado según la finalidad |
| Ciudad | Dato relacionado con la ubicación | Acceso limitado |
| Código postal | Dato relacionado con la ubicación | Acceso limitado |
| Fecha de alta | Dato relacionado con el cliente | Retención definida |

## **3\. Finalidades**

Los datos deben utilizarse de acuerdo con una finalidad específica. El nombre, el correo y el teléfono pueden servir para atender a los clientes; el RFC puede utilizarse para trámites fiscales; y la edad, la ciudad y el código postal pueden servir para generar estadísticas cuando sea necesario.

No se deben utilizar los datos para cualquier propósito solo porque ya están almacenados.

## **4\. Minimización**

No todos los campos son necesarios para cada área. Por ejemplo, el personal de soporte no necesita conocer el RFC si no participa en un trámite fiscal, y el área de analítica puede trabajar con estadísticas sin consultar nombres, correos o teléfonos.

Por eso, se deben limitar los campos disponibles para cada función y evitar recopilar información que no tenga una finalidad justificada.

## **5\. Control de acceso**

Los permisos deben asignarse según las funciones de cada área:

* **Atención al cliente:** consulta los datos necesarios para resolver solicitudes.  
* **Facturación:** accede a la información requerida para los trámites fiscales.  
* **Analítica:** utiliza datos agregados o anonimizados para generar estadísticas.  
* **DBA:** administra la base de datos y sus permisos, con acceso controlado y auditado.  
* **Dirección:** consulta la información necesaria para tomar decisiones, preferentemente mediante reportes.

Se pueden utilizar roles, vistas y permisos específicos para evitar que todos los empleados tengan acceso a la tabla completa.

## **6\. Derechos ARCO**

Los derechos de acceso, rectificación, cancelación y oposición permiten que las personas ejerzan control sobre sus datos personales, de acuerdo con la legislación aplicable.

Técnicamente, la organización debe poder localizar los datos de una persona, corregirlos cuando corresponda, gestionar su cancelación y limitar determinados usos cuando proceda. También debe revisar las copias, los reportes y los sistemas relacionados. El DBA realiza las operaciones técnicas autorizadas, pero no decide por sí solo si una solicitud procede legalmente.

## **7\. Retención**

El periodo de conservación debe establecerse según la finalidad de los datos y las obligaciones legales aplicables. No es correcto conservar toda la información indefinidamente solo porque podría ser útil después.

La organización debe documentar los plazos, revisar los datos que ya no se necesitan y establecer procedimientos para eliminarlos o anonimizarlos cuando corresponda. También debe considerar respaldos, réplicas y exportaciones.

## **8\. Gobierno de datos**

| Responsable | Función principal |
| ----- | ----- |
| DBA | Administrar permisos, respaldos, seguridad técnica y registros de actividad. |
| Responsable de privacidad | Revisar el tratamiento de datos y coordinar el cumplimiento de las políticas de privacidad. |
| Área jurídica | Revisar las obligaciones legales y orientar sobre las solicitudes de derechos ARCO. |
| Propietario de los datos | Definir la finalidad, necesidad y uso autorizado de la información. |
| Desarrolladores | Implementar aplicaciones que utilicen únicamente los datos necesarios y evitar exponer información real en pruebas. |

## **9\. Evaluación integral**

Durante el análisis se identificaron riesgos como el acceso excesivo a los datos, la falta de políticas de retención, el uso de información real en desarrollo y la utilización de datos para finalidades que no están claramente documentadas.

También se identificó la necesidad de proteger los datos sensibles, restringir los permisos, registrar las actividades y evitar que los respaldos o las exportaciones se conviertan en puntos de exposición.

Como controles, se propone utilizar roles y vistas, cifrar la información sensible, anonimizar los datos utilizados para estadísticas y pruebas, definir plazos de conservación y establecer procedimientos para atender solicitudes de los titulares.

## **10\. Conclusiones**

Aprendí que la privacidad y la seguridad están relacionadas, pero no son exactamente lo mismo. Una base de datos puede tener permisos correctamente configurados y aun así presentar problemas si conserva información innecesaria o la utiliza para finalidades no justificadas.

Por eso, es importante diseñar las bases de datos pensando desde el principio en la minimización, el control de acceso, la protección de información sensible, la retención y los derechos de las personas.

# **27\. Preguntas de reflexión**

### **1\. ¿Una base de datos técnicamente segura necesariamente cumple con todos los requisitos de privacidad?**

No, porque también debe respetar la finalidad de los datos, limitar su recopilación y establecer cuánto tiempo se conservarán.

### **2\. ¿Por qué el principio de mínimo privilegio también contribuye a la privacidad?**

Porque cada usuario solo puede consultar la información que necesita, reduciendo la exposición de datos personales.

### **3\. ¿Por qué el DBA no debería decidir por sí solo la finalidad del tratamiento de los datos?**

Porque esa decisión corresponde a los responsables del tratamiento y debe considerar las necesidades del negocio, la privacidad y las obligaciones legales.

### **4\. ¿Por qué los desarrolladores no deberían recibir automáticamente copias completas de bases de datos productivas?**

Porque pueden contener información personal que no necesitan para desarrollar o probar una aplicación.

### **5\. ¿Por qué una copia utilizada para desarrollo también puede representar un riesgo de privacidad?**

Porque puede contener datos reales y quedar expuesta en equipos, archivos o entornos con menos controles de seguridad.

### **6\. ¿Por qué la retención debe formar parte del ciclo de vida de los datos?**

Porque permite definir cuándo los datos dejan de ser necesarios y qué debe hacerse con ellos para evitar conservarlos indefinidamente.

### **7\. ¿Qué relación existe entre privacidad por diseño y diseño de bases de datos?**

La privacidad por diseño consiste en considerar la protección de los datos desde la estructura inicial, definiendo campos necesarios, permisos, medidas de seguridad y plazos de conservación.

### **8\. ¿Qué controles técnicos implementarías para reducir el riesgo de exposición de datos personales?**

Implementaría roles y permisos, vistas restringidas, cifrado, enmascaramiento, auditoría, respaldos protegidos y anonimización para pruebas y estadísticas.

### **9\. ¿Qué información debería conocer un DBA para responder técnicamente a una solicitud ARCO?**

Debe conocer dónde se almacenan los datos, qué tablas y sistemas los contienen, quién tiene acceso y qué respaldos o copias existen para realizar las acciones autorizadas.

### **10\. ¿Qué responsabilidades deberían corresponder al DBA, al responsable de privacidad, al área jurídica y al propietario de los datos?**

El DBA se encarga de las medidas técnicas; el responsable de privacidad coordina la protección de datos; el área jurídica revisa las obligaciones legales; y el propietario de los datos define su finalidad y uso autorizado.

