**Protección de credenciales** 

**¿Qué ocurriría si una persona obtiene acceso de lectura a esta tabla?** pudiera acceder a las contraseñas y credenciales directamente representando un riesgo para las personas y su información.

Generar una representación no reversible

1. **¿Son iguales?** no  
     
2. **Si no son iguales, ¿por qué?** un código tiene una orden de generar aleatoriamente una contraseña nueva asi que cada vez generará algo diferente  
     
3. **¿Qué función cumple gen\_salt()?** es precisamente el que provoca la aleatoriedad en las contraseñas o datos   
     
4. **¿Qué función cumple crypt()?** Calcula el hash de la contraseña utilizando la sal y el algoritmo indicados. Después, ese resultado se puede utilizar para verificar si una contraseña ingresada es correcta.   
     
5. **¿Esto es cifrado reversible?** no el codigo esta diseñado para no recuperarse solo para calcular si la contraseña es correcta

**Verificar una contraseña**

1. **¿Qué resultado obtuviste con la contraseña correcta?** obtuve un true afirmando que la contraseña es correcta   
     
2. **¿Qué resultado obtuviste con la contraseña incorrecta?** el resultado fue un false objetando que la contraseña es incorrecta  
     
3. **¿Por qué no es necesario recuperar la contraseña original?** Porque el sistema puede comprobar si la contraseña es correcta calculando nuevamente el hash   
     
4. **¿Por qué un hash no debe confundirse con cifrado?** Porque el hash es un proceso diseñado para ser irreversible, mientras que el cifrado permite recuperar la información original mediante una clave. 

