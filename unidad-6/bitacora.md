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

#### Análisis del caso de estudio
##### Identifica los roles:
a. ¿Qué clase actúa como la interfaz Observer? ¿Qué método define?
= class Observer, define ~Observer() y onNotify(const std : : string & event)

b. ¿Qué clase actúa como Subject? ¿Qué métodos proporciona para gestionar observadores y notificar?
= class Subject, para gestionar los observadores addObserver(Observer * observer), removeObserver(Observer * observer), para notificar notify(const std : : string & event)

c. ¿Qué clase es el ConcreteSubject en esta aplicación? ¿Por qué? (Pista: ¿Quién envía las notificaciones?)
= class Particle : public Observer, envia las notificaciones con onNotify(const std : : string & event) override

d. ¿Qué clase(s) actúan como ConcreteObserver? ¿Por qué? (Pista: ¿Quién recibe y reacciona a las notificaciones?)
= class ofApp : public ofBaseApp, public Subject.

##### Sigue el flujo de notificacion:
a. Localiza el método keyPressed en ofApp.cpp. ¿Qué sucede cuando se presiona la tecla ‘a’? ¿Qué método se llama?
= Cuando se presiona la 'a' se llama al metodo notify y se le da el string de "attract"

b. Ve al método notify en la clase Subject. ¿Qué hace este método?
= Ese metodo recorre la lista de observadores y en cada uno llama al metodo onNotify

c. Localiza el método que implementa la interfaz Observer en la clase Particle (onNotify). ¿Qué hace este método cuando recibe el evento “attract”?
= Cambia el estado de la particula

##### Registro y eliminacion de observadores
a. ¿En qué parte del código se añaden las instancias de Particle como observadores de ofApp? (Busca dónde se llama a addObserver).
```c++
void Subject::addObserver(Observer * observer) {
	if (!observer) return;
	if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
		observers.push_back(observer);
	}
}
```
b. Aunque no se usa explícitamente en este ejemplo simple, ¿Dónde se eliminarían los observadores si fuera necesario (por ejemplo, si una partícula se destruyera durante la ejecución)? (Busca removeObserver). ¿Por qué es importante el destructor de ofApp en este contexto?
= Es importante en ofApp porque elimina los observadores y libera la memoria de cada particula.
```c++
void Subject::removeObserver(Observer * observer) {
	if (!observer) return;
	observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}
```
##### 1. Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve? 
Su proposito es que un objeto notifique a muchos otros cuando un evento ocurre sin que el primer objeto conozca los detalles de los demas. Resuelve problemas como la union entre quien genera el evento y quien reacciona, vuelve mas facil el agregar nuevos observadores y se centra en un solo notify y no multiples.

##### 2. Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.
![diagrama1](https://github.com/user-attachments/assets/6e2ff010-6be2-4d80-9e33-73dba35903d1)

##### 3. Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.
![diagrama2](https://github.com/user-attachments/assets/d6527b84-0826-414a-a165-f312d01cb86f)

##### 4. ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.
Con el observer, ofApp solo  envia enventos, no necesita conocer que hace cada particula; se encapsula el estado y el comportamiento de la particula.

### Actividad 3

#### Analisis del caso de estudio
##### Identifica la Factory

a. ¿Qué clase actúa como la factory en este ejemplo?
= class ParticleFactory

b. ¿Cuál es el “método factory” específico? ¿Es un método de instancia o estático?
= static Particle * createParticle(const std :: string & type), es estatico.

c. ¿Qué tipo de objeto devuelve este método fábrica?
= Devuelve un puntero, Particle (Particle*).

##### Proceso de creacion

a. Observa el método ParticleFactory::createParticle. ¿Cómo decide qué tipo de partícula específica crear y configurar?
= Segun el string que reciba.

b. ¿Qué información necesita el método fábrica para realizar su trabajo?
= El string type.

c. ¿Qué devuelve si se le pasa un tipo desconocido? ¿Cómo podrías mejorar esto?
= Una particula no personalizada. Lo mejoraria agregando otra condicion que lance un error, de que la particula no cumple con algun parametro conocido.

##### Uso de Factory
 a. ¿Cómo se utiliza la ParticleFactory para poblar el vector particles?
 =

 b. ¿Cómo se vería ofApp::setup si no usara la fábrica y tuviera que crear y configurar cada tipo de partícula (star, shooting_star, planet) directamente usando new Particle() y luego ajustando sus propiedades (size, color, velocity)?
 = 

##### 1. Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?
Es para crear objetos sin tener que estar repitiendo el new mas lo demas; ademas se crean los objetos en el mismo lugar y permite encapsular variantes tras una interfaz uniforme.

##### 2. ¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí?
Es mas facil para leer, la inicializacion esta en un solo lugar y si se requieren cambios solo se cambia la factory, garantiza que todo se crea de forma coherente.

##### 3. Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?
En esta seccion del codigo:
```c++
Particle * ParticleFactory::createParticle(const std::string & type) {
	Particle * particle = new Particle();

	if (type == "star") {
		particle->size = ofRandom(2.0f, 4.0f);
		particle->color = ofColor(255, 0, 0);
	} else if (type == "shooting_star") {
		particle->size = ofRandom(3.0f, 6.0f);
		particle->color = ofColor(0, 255, 0);
		particle->velocity *= 3.0f;
	} else if (type == "planet") {
		particle->size = ofRandom(5.0f, 8.0f);
		particle->color = ofColor(0, 0, 255);
	}
	return particle;
}
```
Agregaria otro else if, con particle->size = ofRandom(10.0f,15.0f); particle->color = ofColor(0,0,0); particle->velocity *= 0.1f;
No modificaria el ofApp::setup() ya que lo estoy implementando en la factory.

##### 4. El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?.
Se puede llamar sin instanciar una factory y es bueno cuando la factory no necesitaestado.
No permite herencia o polimorfismo, es mas complejo si se quiere qaue mantenga un cache o un contador.

#### Autoevaluación 
3, ya que realice una actividad completa y esta autoevaluación.
