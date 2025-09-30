# Bitácora de aprendizaje de la unidad 6

### Actividad 1

##### 1. ¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.
   
Para interacrtuar con la aplicación se utilizan las teclas 'a','s','n','r'.  
Al presionar la 'a' las partículas comienzan a dirigirse hacía el mouse, desde cualquier lugar de la pantalla.  
Al presionar la 'r' las partículas comienzan a huir del mouse.  
Al presionar la 's' todas las partículas se detienen en el lugar de la pantalla que esten, si se pasa el mouse cerca de estas no pasa nada. Por ultimo, cuando se presiona la 'n' las partículas vuelven a su estado "natural", divagan por la pantalla sin orden alguno.

##### 2. ¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?

No noto la diferencia entre las partículas, diferencias tales que no sean ni su tamaño, color o velocidad. Todas se comportar de manera random al inicio, no tienen un patron de movimiento ni se ven afectadas por el mouse, al presionar alguna tecla que tenga interacción con el mouse y las partículas, pues sucede lo que tenga que pasar segun la tecla presionada. 

##### 3. Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.

**_Estado Inicial_**<img width="1024" height="765" alt="Cap1" src="https://github.com/user-attachments/assets/7c849d18-8be6-42e9-8615-96c02ebf6ad0" />  

**_Luego de presionar 'a'_**<img width="1024" height="764" alt="Cap2" src="https://github.com/user-attachments/assets/6fc27196-a8a0-4d60-bcbf-2faa11198c11" />  

**_Luego de presionar 'r'_**<img width="1024" height="765" alt="Cap3" src="https://github.com/user-attachments/assets/286d32af-5fa7-4b6c-b5eb-b0d1e73f0508" />  

**_Luego de presionar 's'_**<img width="1021" height="766" alt="Cap5" src="https://github.com/user-attachments/assets/bed8f954-89e2-42c8-8b85-08dab06fa199" />  

**_Luego de presionar 'n'_**<img width="1024" height="767" alt="Cap4" src="https://github.com/user-attachments/assets/75da6e8c-f956-4bf1-bb85-6ea28f03c82a" />

##### 4. ¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.

Primero creo que hay una variable que toma el valor en X y Y del mouse, al presionar la tecla 'a' la variable que le da el movimiento a las partículas cambia para que persigan las coordenadas del mouse; al presionar la tecla 'r' pasaría lo contrario, la variable del movimiento de las particulas ordena que se alejen de las coordenadas del mouse; al presionar la 's' simplemente congelo en el lugar donde estan las partículas; y al presionar la 'n' le doy nuevamente a la variable del movimiento un random.

### Actividad 2

##### Análisis del caso de estudio



##### 1. Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve? 

##### 2. Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.

##### 3. Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.

##### 4. ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.
