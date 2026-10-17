**Analizar un escenario de seguridad**  
 

1. **¿Cuáles son los principales riesgos?** casi todo lo que puede salir mal está allí. mantiene todo la información sensible expuesta y fácil para el uso de cualquier persona externa o ajena   
     
     
2. **¿Qué mecanismo utilizarías para cada elemento?**  
   Nombre y correo: control de acceso y permisos.  
   Contraseña: hash seguro con Argon2 o bcrypt.  
   RFC: cifrado simétrico.  
   Información financiera: cifrado y control de acceso.  
   Claves criptográficas: gestor de secretos.  
   Conexiones: TLS con validación del servidor.  
   Respaldos: cifrado y acceso restringido.

3. **¿Cuál de los problemas consideras más crítico y por qué?**  
    El almacenamiento de contraseñas en texto claro, porque si alguien accede a la base de datos podría verlas y usarlas para entrar a las cuentas.   
     
     
4. **¿Tener correctamente configurados los usuarios y permisos elimina estos riesgos?**  
   a medias, porque no evitan que los datos estén expuestos por falta de cifrado o por un mal manejo de las claves. 

