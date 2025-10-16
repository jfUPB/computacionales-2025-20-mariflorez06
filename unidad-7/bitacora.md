# Bitácora de aprendizaje de la unidad 7

## Fase Set 💡

### Actividad 1

##### 1. Captura de pantalla del ejemplo funcionando.

<img width="665" height="455" alt="cap2" src="https://github.com/user-attachments/assets/3503b68c-60d5-4f73-a5df-6c8f89cad1f5" />
<img width="580" height="719" alt="cap1" src="https://github.com/user-attachments/assets/3c1c3496-9791-4317-92c1-9b40f143831f" />
<img width="118" height="432" alt="cap5" src="https://github.com/user-attachments/assets/2c16d8e5-0a36-40a6-ae38-e1083d51bfcb" />
<img width="416" height="406" alt="cap3" src="https://github.com/user-attachments/assets/e4d57bf0-6305-4647-b7be-fcd053b41156" />
<img width="346" height="120" alt="cap4" src="https://github.com/user-attachments/assets/c40a7448-4765-416a-9e50-e837cb8a4879" />

##### 2. ¿Qué preguntas te surgen al ver el código?

a) ¿Qué es VAO/VBO?
b) ¿Qué es buffer?

### Actividad 2

**GLFW** crea la ventana y maneja el teclado y el mouse (Crea ventana), **opengl32.lib** inicia el OpenGL y crea el contexto (Inicia todo), **GLAD** carga funciones modernas de OpenGL desde los drivers de la GPU (Carga OpenGL), **GLM** hace las matematicas 3D y puede utilizar vectores y matrices (Hace cuentas); y los **Drivers de la GPU** contienen las funciones reales del OpenGL moderno

## Fase Seek 🔎

### Actividad 3

Primer Experimento. glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2);
= Al compilar y al abrirse la ventana, lo que aparece es que el triangulo naranja no esta en el centro de la ventana, sino a un lado.<img width="199" height="199" alt="exp 1" src="https://github.com/user-attachments/assets/4bdcb7aa-b6e0-4425-860b-5ce9965c0a70" />


Segundo Experimento. glViewport(0, bufferHeight / 2, bufferWidth / 2, bufferHeight * 2);
= Al compilar y al abrise la ventana, lo primero que aparece es la ventana sin triangulo, luego al hacer mas grande la ventana si aparece con normalidad. <img width="200" height="199" alt="exp 2" src="https://github.com/user-attachments/assets/89f6a1e8-87d6-4be6-a04a-3aa1414e25ea" />


Tercer Experimento. glViewport(0, bufferHeight / 2, bufferWidth / 4, bufferHeight * 2);
= Al compilar y al abrise la ventana, lo primero que aparece es la ventana sin triangulo, luego al hacer mas grande la ventana si aparece con normalidad. <img width="200" height="199" alt="exp 3" src="https://github.com/user-attachments/assets/a5a9200e-45c8-42d7-a245-4a3b323b51ea" />


Cuarto Experimento. glViewport(0, bufferHeight / 2, bufferWidth / 2, bufferHeight * 4);
= No deja compliar, aparece un error. <img width="313" height="131" alt="exp 4" src="https://github.com/user-attachments/assets/d97e7551-2861-446f-a423-b7ec90f7fbca" />

**Resumen** El entorno de OpenGL es el "estudio" donde OpenGL guarda es estado de los shaders, las texturas, el buffer; la version que uno usa y la conexion con la ventana. Sin ese contexto, las funciones no saben donde dibujar ni que recursos existen.

### Auto evaluacion
Mi nota es un 2, ya que solo realice tres actividades y la autoevaluacion, me parecio un poco complicada la unidad por la cantidad de informacion y cosas nuevas que nos enseñan, y al estar creando el proyecto me perdi un poco bastante.






