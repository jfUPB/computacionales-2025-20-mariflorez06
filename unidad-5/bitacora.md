# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**
### Actividad 1
1. ¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.
= Se trata de privatizar los atributos de una clase para tener acceso a ellos desde un método público.

2. ¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.
= Una herencia es darle a una clase nueva los atributos y métodos de otra. Sirve para no sobrescribir código. Es como tener una clase general, por ejemplo Mascota, que tenga atributos como nombre y edad, y la herede a clases como Gato y Perro, que tengan métodos como Ronronear y Ladrar respectivamente. La clase Gato y Perro además de los métodos que tienen, tendrán los atributos de la clase Mascota.

3. ¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.
= El polimorfismo me deja crear un método de una clase base, que será heredada por otras clases y funcionará diferente en cada una de ellas.

- Qué es?
= 
° public abstract class: es una clase que no se puede instanciar directamente (no puedes crear objetos de ella). Sirve como una plantilla o base para otras clases que sí la heredan. 
° public abstract void: Obliga a las subclases a definir cómo funciona ese método.  
° public override void:  Indica que este método sobrescribe (reemplaza) la implementación de un método con la misma firma que está definido en una clase base .
° public double: Es el tipo de dato que representa un número decimal de doble precisión (número con decimales).  
° foreach: Sirve para recorrer todos los elementos de una colección uno por uno y realizar una acción con cada uno de ellos.

##### Encapsulamiento:
1. Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.
=
```c# 
private string nombre;

  public string Nombre
  { 
     get { return nombre; }
     protected set { nombre = value; }
  }
```
2. ¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?
=

##### Herencia:
1. ¿Cómo se evidencia la herencia en la clase Circulo? Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?
= Circulo hereda la propiedad de Nombre y la clase Dibujar()

##### Polimorfismo:
1. Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿Cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta, solo quiero que intentes razonar cómo podría ser.
=

##### 1. Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?
= Se crea un espacio en el heap que dentro tiene otros espacios donde se guardan la base, la altura y el nombre.

##### 2. El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.
=

##### 3. La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?
= Es una proteccion que realiza el compilador, si se intenta acceder a un private desde afuera, el compilador falla y no se ejecuta.

### Actividad 2
<img width="883" height="716" alt="CAP1" src="https://github.com/user-attachments/assets/dfb79237-9e36-424b-b7b6-252e661807a2" />
<img width="1025" height="624" alt="CAP2" src="https://github.com/user-attachments/assets/5daba8c1-b76c-4b20-bab5-51b2a29847cb" />
<img width="986" height="761" alt="CAP3" src="https://github.com/user-attachments/assets/91975769-f075-42a9-abd9-eac988399cc9" />

## 2.  **La pregunta inicial**

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
##### Autoevaluacion
Mi nota es 2 ya que realmente no le dedique el tiempo necesario a realizar el camino que habia elegido, no pude organizar mi tiempo para poder hacerlo en las horas por fuera de la clase y en clase no era mucho lo que adelantaba. Con el poco tiempo que le proporcione, pude entender varias cosas, pero aun me quedan un poco de vacios con respecto al poliformismo, siento que se como funciona pero al momento de que me toque explicarlo, no sabria muy bien como hacerlo.  

Igualmente, considero que este metodo de trabajo es mejor, si es verdad que depende muchisimo mas de uno mismo, pero si me hace deber crear un habito de estudio mayor para esta materia.
