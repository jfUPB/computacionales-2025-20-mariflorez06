# Unidad 1
## Fase: Set-Seek 💡🔎
### Actividad 1
- Ciclo feetch-decode-execute
```asm
@1
D=A
@2
D=D+A
@16
M=D
@END
(END)
0;JMP
```
- Notas:
  
A (addres-direcciones) y D son 'variables', @1 guarda el valor en A, M es la memoria y guarda el dato en la memoria RAM, el apartado de PC me dice que instrucción esta leyendo y va a ejecutar, incrementa de uno en uno; (0;JMP) es una dirección en la ROM, JMP es jump (salto) y lo realiza a la posición guardada en A, 0 es una operación; (END) es una etiqueta y da la posición en la que está, es decir, el @END me pondrá un @7 en la posición 6.ROM guarda la receta/instrucciones, RAM hoja en blanco.

- Experimento:
```asm
@5
D=A
@10
D=D+A
@20
M=D
@END
(END)
0;JMP
```
- Pregunta:
  
  1. Qué diferencia hay entre los datos almacenados en la RAM y en la ROM?
     
  = La RAM me permite acceder de manera rápida, pero solo almacena datos y programas que se usan en la actualidad, una vez apagues el equipo, estos datos se borrarán. La ROM por el contrario solo permite leer los datos, no modificarlos o escribirlos; y al apagar el equipo los datos o programas quedaran almacenados.

### Actividad 2
- Preguntas:
  
  1. Identifica una instrucción que use la ALU y explica qué hace.
     
      D=D-A. Le resta a D el valor de A y vuelve a almacenarlo en D.       
  2. ¿Para qué sirve el registro PC?
     
     Es un contador que indica que instruccion sera leida a continuacion.
  
  3. ¿Cuál es la diferencia entre @i y @READKEYBOARD?
     
     @i es una variable que es asignada en la memoria RAM comenzando en el 16, es decir, si luego hago @j este quedara en la posicion 17 de la RAM. @READKEYBOARD es una etiqueta de un dato en la ROM, cuando esta etiqueta se usa, se vuelve a la parte del codigo donde esta fue etiquetada.
  
  4. Describe qué se necesita para leer el teclado y mostrar información en la pantalla.
     
     Para leer el teclado se utiliza la etiqueta @KBD y D=M, que carga en D el registro del teclado, si M=0 el codigo sigue, pero si en M hay algo diferente a 0, salta al codigo de @KEYPRESSED. Y para leerlo se utiliza el @SCREEN que apaga y prende pixeles.
     
  5. Identifica un bucle en el programa y explica su funcionamiento.
      
      @READKEYBOARD  0;JMP marcan el bucle. Comienza en (READKEYBOARD) y empieza leyendo el teclado, si hay tecla salta al @KEYPRESSED si no, sigue leyendo el codigo; luego hace comprobaciones con @i y @SCREEN, si @i es muy pequeno D;JLE salta al inicio, sino decrementa @i y apaga los pixeles M=0. Y vuelve a (READKEYBOARD).
     
  6. Identifica una condición en el programa y explica su funcionamiento.
      
      D;JNE = Si el valor de D No es Igual A 0, salta.
     
      D;JLE = Si el valor de D Es Menor o Igual a 0, salta.
     
      D;JGE = Si el valor de D es Mayor o Igual a 0, salta.

## Fase: Apply 🛠️
### Actividad 3
- Control de flujo con saltos
```asm
(LOOP)
@5
D=M
@10
D=D-A

@MENOR
D;JLT

(MAYOR)
@7
M=0
@LOOP
0;JMP

(MENOR)
@7
M=1
@LOOP
0;JMP
```
### Actividad 4
- Implementando un ciclo simple
```asm
@12
M=0

@1
D=A
@13
M=D

(LOOP)
@13
D=M
@5
D=D-A
@END
D;JGT

@13
D=M
@12
M=D+M

@13
M=M+1

@LOOP
0;JMP

(END)
@END
0;JMP
```
## 🤔 Fase: Reflect

### Autoevaluación
#### Parte 1
##### 1. Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?
  Fetch-Decode-Execute es el ciclo que se hace siempre al momento de leer un "código". Es practicamente que el programa busca o lee la instrucción, luego decodifica esa información y entiende lo que dice instrucción, y luego ejecuta la instrucción dando una respuesta.
  El PC en este ciclo seria la fase Fetch, porque es el que dice que instrucción es la siguiente a leer.
##### 2. ¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.
  Una instrucción A (@) puede ser tanto para darle un valor a 'A' o para "traer" una etiqueta.
  Ejemplo: 
``` asm
@7
(LOOP)
@LOOP
```
  Una instrucción C es para "coger" un valor, realizar una operación, poner un valor en alguna parte de la memoria.
  Ejemplo:
``` asm
D=D-A
M=D
D=M
```
##### 3. Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.
  El registro A es donde "cae" la indicación de la instrucción A, el registro D guarda datos temporales.
##### 4. ¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).
  Los saltos primero hacen una operación y luego si realiza el salto co la condición. 
``` asm
D;JGT.
```
##### 5. ¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero)
  Se hace implimentando saltos con condiciones y con etiquetas.
##### 6. ¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?
  D=M Es para guardar el valor de D en la RAM, en cambio M=D es para coger el valor que esta en la RAM y ponerlo en D.
##### 7. Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).
  Hay que crear primero la etiqueta y luego ponerla en alguna parte de las instrucciones, ya que KBD y SCREEN son valores de la memoria RAM que ya vienen prederterminados.

#### Parte 2
##### 1. ¿Cuál fue el concepto o actividad más desafiante de esta unidad para ti y por qué?
  La actividad 2 fue un poco más complicada para entender, por los valores predeterminados, porque ya involucraba el teclado y saltos que no habiamos visto. Pero luego de que el profe la revisara en clase, todo quedó bastante claro.
##### 2. La metodología de “predecir, ejecutar, observar y reflexionar” fue central en nuestras actividades. ¿En qué momento esta metodología te resultó más útil para entender algo que no tenías claro?
  Al momento de realizar junto al profe la actividad 3, al él utilizar esa metodología se hizo más fácil el explicarnos el por qué de las cosas y cómo podiamos ir resolviendo el problema que nos habian propuesto.
##### 3. Describe un momento “¡Aha!” que hayas tenido durante estas dos semanas. ¿Qué estabas haciendo cuando ocurrió?
  Quizas el entender por completo la actividad 2.
##### 4. Pensando en la próxima unidad, ¿Qué harás diferente en tu proceso de estudio para aprender de manera más efectiva?
  Mejoraría mi manejo del tiempo, no en clase, sino por fuera de ella.

### FeedBack
##### 1. Continuar: ¿Qué aspecto de las actividades, las explicaciones o la dinámica de la clase te ha resultado más útil o te ha gustado más y debería seguir haciendo?
  Me gusta mucho como explicas paso a paso todo, que nos cuestiones sobre cosas que pueden o no pasar en las actividades, y que estes muy pendiente de quienes necesiten ayuda o tengan dudas.
##### 2. Dejar de hacer: ¿Qué aspecto de la unidad te ha resultado confuso, poco útil o frustrante? ¿Hay algo que crees que debería eliminar o cambiar drásticamente?
  Creo que toda la unidad es bastante entendible y te va subiendo progresivamente el nivel de dificultad.
##### 3. Empezar a hacer: ¿Qué te habría gustado que hiciéramos que no hicimos? ¿Tienes alguna idea para una actividad o un recurso que podría mejorar el aprendizaje en la próxima unidad?
  No tengo comentarios para esta parte, me parece que todo esta bien.
##### 4. Ritmo y Dificultad: en una escala del 1 (muy fácil/lento) al 5 (muy difícil/rápido), ¿Cómo calificarías el ritmo y la dificultad general de esta unidad? ¿Por qué?
  El ritmo seria un 4 o 5, ya que el tener entregas entre la misma semana, con solo un día de diferencia, nos obliga a sacar tiempo que muchas veces no tenemos por trabajos de otras materias, por actividades extracurriculares o simplemente cosas personales. Siento que la forma de partir la unidad en varias partes esta bien, pero quizas seria más util, cómodo  y menos estresante poder tener las fases abiertas durtante toda la unidad.
  La dificultad un 3, me parece que toda la unidad es fácil de comprender y de poner en práctica.
  
  



