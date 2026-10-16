# **Informe del laboratorio**

## **Clasificación**

Los datos de la tabla `clientes` requieren protección porque algunos permiten identificar directamente a una persona, como el nombre, correo electrónico, teléfono y RFC. Otros datos, como la edad, ciudad, código postal y fecha de alta, pueden ayudar a identificarla cuando se combinan entre sí. Por eso, es importante revisar qué información necesita cada usuario y limitar el acceso a los datos que no sean necesarios para sus actividades.

## **Enmascaramiento**

En esta actividad se ocultó parcialmente el correo electrónico, teléfono y RFC de los clientes, dejando visibles el ID y el nombre. Esto se hizo para el área de soporte, ya que puede necesitar consultar información básica sin tener acceso a todos los datos completos.

Para conseguirlo, se creó la vista `v_clientes_soporte`, utilizando funciones de PostgreSQL para reemplazar parte de los datos por asteriscos. También se configuraron permisos para que el rol `soporte` pudiera consultar la vista, pero no tuviera acceso directo a la tabla original. De esta manera, se limita la información que puede visualizar ese usuario.

## **Seudonimización**

Para realizar la seudonimización se generaron tokens UUID mediante la función `gen_random_uuid()` de PostgreSQL. Cada token se relacionó con el ID original de un cliente y esa correspondencia se guardó en la tabla `pii.mapa_cliente`.

Después, se creó la tabla `analitica.clientes`, que contiene los tokens y otros datos necesarios para realizar análisis, sin incluir directamente el nombre, correo, teléfono ni RFC.

El mapa de correspondencia debería estar disponible únicamente para personal autorizado que realmente necesite recuperar la relación entre un token y un cliente. Por eso, se separaron los permisos del analista para impedir que consulte el mapa y la tabla original. Así se aplica el principio de mínimo privilegio y se reduce el riesgo de que se identifique a los clientes sin autorización.

## **Anonimización**

En esta actividad se generaron consultas estadísticas sin mostrar directamente los identificadores personales, como el nombre, correo, teléfono y RFC. También se generalizaron algunos atributos: la edad se agrupó en rangos y el código postal se redujo a sus dos primeros dígitos para representar una región.

Después, se combinaron el rango de edad y la región para observar cuántos registros había en cada grupo. Finalmente, se utilizó `HAVING COUNT(*) >= 5` para excluir los grupos que no alcanzaran cinco registros.

Sin embargo, esto no garantiza que los datos sean completamente anónimos, porque la combinación de atributos todavía podría permitir identificar a una persona. Además, si los grupos son demasiado pequeños, se pierde privacidad y aumenta el riesgo de reidentificación.

## **Retención**

Para revisar la retención se utilizó como criterio un periodo de cinco años, identificando los registros cuya fecha de alta fuera anterior a ese plazo. La consulta únicamente permite encontrar los registros que podrían ser candidatos a revisión, sin eliminarlos de la tabla principal.

La información debería conservarse mientras siga siendo necesaria para la finalidad establecida o exista una obligación legal que lo justifique. Los datos que ya no sean necesarios podrían eliminarse, siempre que se haya comprobado que no existe una razón válida para mantenerlos.

Antes de eliminar información, deberían existir una autorización del responsable, una política de conservación, una copia de seguridad verificada y un registro de la operación. También tendría que existir un procedimiento para recuperar los datos si ocurre algún error.

## **Conclusiones**

Para el área de soporte utilizaría el enmascaramiento mediante una vista, porque permite consultar información útil sin mostrar todos los datos personales.

Para el área de analítica utilizaría la seudonimización, porque permite trabajar con los registros mediante tokens sin incluir directamente los identificadores de los clientes. El acceso al mapa de correspondencia tendría que mantenerse restringido.

Para publicar estadísticas utilizaría la anonimización, generalizando los atributos y suprimiendo grupos pequeños para reducir la posibilidad de identificar a las personas.

Ninguna de estas técnicas sustituye al control de acceso, porque la protección de los datos también depende de quién puede consultar la información y qué permisos tiene. Aunque los datos estén enmascarados, seudonimizados o generalizados, es necesario establecer restricciones para evitar accesos no autorizados.

# **Preguntas de reflexión**

**1\. ¿Cuál es la diferencia entre enmascaramiento y seudonimización?**

El enmascaramiento oculta parte de un dato para que no se muestre completo, mientras que la seudonimización reemplaza los identificadores originales por otros valores, como tokens. En el primer caso se limita lo que se visualiza y, en el segundo, se busca separar la identidad de los datos utilizados.

**2\. ¿Por qué la seudonimización no significa anonimización?**

Porque todavía existe un mapa que permite relacionar los tokens con los identificadores originales. Si alguien obtiene acceso a ese mapa y a la información necesaria, puede volver a identificar a los clientes.

**3\. ¿Por qué eliminar `nombre` y `RFC` no garantiza que un conjunto de datos sea anónimo?**

Porque todavía pueden quedar otros datos, como la edad, ciudad y código postal, que al combinarse pueden ayudar a identificar a una persona. Por eso, eliminar los identificadores directos no siempre es suficiente.

**4\. ¿Qué función tienen los cuasi-identificadores?**

Son atributos que por sí solos normalmente no identifican directamente a una persona, pero que combinados pueden reducir el grupo de personas al que pertenece un registro. Algunos ejemplos son la edad, la ubicación y la fecha de alta.

**5\. ¿Por qué es importante separar el mapa de seudonimización?**

Porque contiene la relación entre los tokens y los identificadores originales. Si cualquier analista pudiera consultarlo, sería más fácil relacionar los datos analíticos con personas específicas.

**6\. ¿Qué principio de seguridad se aplica al impedir que el analista acceda al mapa?**

Se aplica el principio de mínimo privilegio, que consiste en conceder a cada usuario solamente los permisos que necesita para realizar sus actividades.

**7\. ¿Por qué una vista puede ser preferible a entregar acceso directo a la tabla?**

Porque una vista permite mostrar únicamente los campos necesarios y ocultar parte de la información. Así, el usuario puede realizar sus actividades sin consultar directamente todos los datos almacenados en la tabla original.

**8\. ¿Qué diferencia existe entre proteger un dato para visualización y protegerlo contra acceso no autorizado?**

Proteger un dato para visualización significa limitar la información que se muestra, por ejemplo, ocultando parte de un teléfono. Protegerlo contra accesos no autorizados significa establecer permisos para impedir que usuarios sin autorización puedan consultar la información original.

**9\. ¿Por qué la retención forma parte de la protección de datos?**

Porque conservar información durante más tiempo del necesario aumenta la cantidad de datos que podrían quedar expuestos ante un acceso indebido. Establecer periodos de conservación ayuda a controlar qué información sigue siendo necesaria y cuál debe revisarse para su posible eliminación.

**10\. ¿Qué riesgo existe si una organización conserva información indefinidamente?**

Existe el riesgo de que se acumulen datos que ya no son necesarios y que puedan exponerse, utilizarse indebidamente o consultarse sin autorización. Además, conservarlos indefinidamente puede incumplir las políticas de la organización o las obligaciones legales aplicables.

