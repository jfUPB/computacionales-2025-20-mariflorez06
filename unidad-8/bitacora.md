# Bitácora de aprendizaje de la unidad 8

## Fase Set 💡

### Actividad 1

a) Ejecuta el programa y haz clic en la ventana. Observa lo que sucede.  

= Al ejecutar el programa se ve una ventana con un circulo negro que pasa a la misma velocidad de izquierda a derecha. Al hacer click sobre la ventana, esta se pausa, cambia el tamaño del circulo y continua.

b) Ejecuta el programa y haz clic en la ventana. Observa que el programa ahora no se congela, pero el círculo no cambia de tamaño inmediatamente.  

= Al ejecutar el programa se ve la misma ventana con el circulo negro. Al hacer click sobre la ventana, esta sigue el movimiento y de repente cambia el tamaño del circulo.

c) Explica la diferencia entre concurrencia y paralelismo. ¿Por qué es importante entender esta diferencia al trabajar con hilos?  

= En el paralelismo todas las tareas se ejecutan a la mima vez, todas en el mismo tiempo; en cambio en la concurrencia, todas las tareas se ejecutan una tras otra en periodos cortos.

## Fase Seek 🔎

### Actividad 2

a) ¿En qué partes del código se está protegiendo el acceso a la variable circleSize?
```c++
lock();
ofSeedRandom();
circleSize = ofRandom(20, 70);
unlock();
```
b) ¿Qué ocurre con el rendimiento del programa? ¿Es posible que el rendimiento se vea afectado por el uso de mutex? ¿Por qué?  

= Si, el rendimiento se afecta al sincronizar el acceso con mutex, ya que al intentar acceder varios hilos a un recurso protegido, reduce el paralelismo y causa esperas, ya que solo uno puede hacerlo a la vez.

c) ¿Qué ocurre si cambias el valor de la variable useLock? ¿Por qué crees que ocurre esto?  

= Con TRUE
1. Estado Inicial y luego de darle 'r'
<img width="295" height="114" alt="true1" src="https://github.com/user-attachments/assets/1c412238-9dfc-4883-8a3f-9c022e236388" />

2. Luego de darle 's', al darle dos veces vuelve al estado inicial
<img width="295" height="116" alt="true2" src="https://github.com/user-attachments/assets/1aafa2f4-3c8e-4c53-a5f4-175470217313" />

4. Luego de darle 's' y 'r'
<img width="293" height="116" alt="true3" src="https://github.com/user-attachments/assets/50fba86f-221d-43ae-b729-920a56c74ac5" />

Con FALSE
1. Estado inicial, vuelve a este al presionar 's' dos veces
<img width="244" height="105" alt="false1" src="https://github.com/user-attachments/assets/57bfee3c-6500-4960-93c2-589ade733a0b" />

2. Luego de darle 's'
<img width="242" height="104" alt="false2" src="https://github.com/user-attachments/assets/80cf1225-42d1-4308-8ac7-4cb9db0a2fb7" />

3. En estado inicial y luego dar 'r'
<img width="242" height="106" alt="false3" src="https://github.com/user-attachments/assets/8922b54d-4478-47d5-b945-7e5ed322ad92" />

d) ¿Cómo puede presentarse la condición de carrera en este caso?  

= Se ve que en el counter no llega el valor esperado y cambia entre ejecuciones, el resultado no es determinista y suele ser menor a lo esperado

e) ¿Qué es lo que está pasando?   

= La instruccion tiene dos hilos que intercalan los pasos, ambos leen el mismo valor, ambos incrementan y ambos escriben, de modo de que una de las actualizaciones se pierde.

### Actividad 4

a) ¿Cuál es la estructura de datos principal que contiene la información de todos los boids y que es accedida por múltiples hilos (el hilo principal para dibujar, el hilo trabajador para actualizar)?  

= El *std::vector<Boid> boids* dentro de la clase *Flock* es el contenedor que guarda todas las instancias de *Boid* y es accedido por el hilo trabajador y el principal.

b) Localiza todas las llamadas a lock() y unlock() dentro de la clase Flock (o donde se acceda al vector compartido).  

= 
1. Flock::addBoid(int x,int y) → lock(); boids.emplace_back(...); unlock();

2. Flock::threadedFunction() → lock(); for (Boid& b : boids) { b.run(boids); } unlock();

3. ofApp::draw() → flock.lock(); for (...) b.draw(); flock.unlock();

c) ¿Puedes intuir por qué tener muchos hilos esperando para adquirir un lock sobre el mismo vector (alta contención) podría limitar el beneficio de rendimiento del paralelismo en este caso?  

= Si muchos hilos compiten por el mismo lock, entonces los hilos quedan en espera en lugar de trabajar en pararlelo, la espera mas el cambio de contexto genera mas gasto, y como resultado el paralelismo se pierde y el rendimiento puede quedarse debajo de lo ideal.

d) Analiza el código del Flocking sin hilos y el Flocking con hilos. ¿Qué diferencias encuentras? ¿Por qué crees que es importante la sincronización en el segundo caso?  

= 
1. Sin hilos: Todo actualiza y dibuja en el mismo hilo, no hay accesos recurentes entonces no se necesitan locks.
2. Con hilos: La actualizacion esta separada por un hilo trabajador y el dibujo o la entrada en un hilo principal, esto introduce concurrencia, ademas es imprescindible sincronizar el acceso oara evitar condiciones de carrera.

e) Notaste que la versión con hilos tiene un sleep(5) en el hilo trabajador. ¿Por qué crees que se ha añadido? ¿Qué pasaría si lo eliminamos  

= El trabajador se actualiza constantemente, adquiriendo locks muy seguido, el hilo principal puede quedar bloqueado mas a menudo.

f) ¿Qué pasaría si no se usaran? ¿Cómo afectaría esto al comportamiento del programa?  

= Las condiciones de carrera producirian lecturas inconsistentes, se pierden actualizaciones; aveces no se manifestara pero seguira habiendo riesgo y fallos dificiles de depurar.

g) ¿Qué ocurre si mientras el hilo trabajador está calculando el movimiento de los boids, el hilo principal intenta añadir un nuevo boid? ¿Se congelará la aplicación? ¿Por qué?  

= No se produce un "congelamiento: indefinido, simplemente se bloquearia hasta que el worker haga el unlock.

## Fase Apply 🛠️

### Actividad 5

a) Pega la parte clave de tu función modificada que calcula el píxel para el conjunto de Julia.
```c++
// Dentro de MandelbrotThread (método private)
int calculatePixel(int x, int y) {
    // Mapeo de píxel a plano complejo
    float px = ofMap(x, 0, imgWidth, -2.0f, 1.0f);
    float py = ofMap(y, 0, imgHeight, -1.5f, 1.5f);

    float zx, zy, cx, cy;
    if (useJulia) {
        // --- JULIA: z = pixel, c = juliaK ---
        zx = px;
        zy = py;
        cx = juliaK.x;
        cy = juliaK.y;
    } else {
        // --- MANDELBROT: z = 0, c = pixel ---
        zx = 0.0f;
        zy = 0.0f;
        cx = px;
        cy = py;
    }

    int iterations = 0;
    while (zx * zx + zy * zy < 4.0f && iterations < maxIterations) {
        float tmp = zx * zx - zy * zy + cx;
        zy = 2.0f * zx * zy + cy;
        zx = tmp;
        iterations++;
    }
    return iterations;
}
```

b) Muestra cómo mapeaste la posición del mouse a la constante k.
```c++
// en ofApp::mouseMoved(int x, int y)
juliaK.x = ofMap(x, 0, ofGetWidth(),  -1.5f, 1.5f);
juliaK.y = ofMap(y, 0, ofGetHeight(), -1.5f, 1.5f);

// y luego forzamos recálculo si estamos en modo Julia
if (useJulia) startCalculation();
```

c) Describe brevemente cómo reutilizaste la estructura de hilos de la versión Mandelbrot. ¿Tuviste que cambiar mucho esa parte?  

= Reutilice casi toda la estructura del Mandelbrot, cambie solo la funcion de calculo *calculatePixel* para aceptar la lógica Julia/Mandelbrot y añadí referencias juliaK y useJulia en el constructor del thread.

d) ¿Cómo te aseguraste de que la imagen se recalculara cuando el mouse se movía?  

= Cada vez que se mueve el mouse, se llama a: *startCalculation();*. Esto detiene los hilos activos, actualiza los valores de kx y ky, inicia nuevos hilos que recalculan la imagen con el nuevo valor de k y asi, el fractal se actualiza en tiempo real segun el movimiento del mouse.

e) Incluye al menos dos capturas de pantalla que muestren diferentes fractales de Julia generados al mover el mouse en tu aplicación.
= https://github.com/user-attachments/assets/ff6c4b60-3b84-470b-b5df-257ecc17f5f2

f) ¿Encontraste algún desafío particular al implementar la interacción o modificar el cálculo?  

= Mantener el rendimiento mientras se recalcula continuamente con cada movimiento del mouse y ajustar los rangos del mapa para obtener patrones sin que el fractal desapareciera.

Codigo ofApp.h:
```c++
#pragma once

#include "ofMain.h"
#include "ofThread.h"
#include <thread>
#include <vector>

// -----------------------------
// Mandelbrot / Julia worker
// -----------------------------
class MandelbrotThread : public ofThread {
public:
	MandelbrotThread(int startY, int endY, int width, int height, int maxIter, ofPixels & pixelsRef,
		ofVec2f & juliaKRef, bool & useJuliaRef)
		: startRow(startY)
		, endRow(endY)
		, imgWidth(width)
		, imgHeight(height)
		, maxIterations(maxIter)
		, pixels(pixelsRef)
		, juliaK(juliaKRef)
		, useJulia(useJuliaRef) {
	}

	void threadedFunction() override {
		for (int y = startRow; y < endRow && isThreadRunning(); ++y) {
			for (int x = 0; x < imgWidth; ++x) {
				int iterations = calculatePixel(x, y);
				pixels.setColor(x, y, mapIterationsToColor(iterations));
			}
		}

		ofLogVerbose("MandelbrotThread") << "Hilo para filas " << startRow << "-" << endRow << " terminado.";
	}

private:
	int startRow, endRow;
	int imgWidth, imgHeight;
	int maxIterations;
	ofPixels & pixels;
	ofVec2f & juliaK; // referencia a la constante k (para Julia)
	bool & useJulia; // referencia a la bandera que decide Julia vs Mandelbrot

	int calculatePixel(int x, int y) {
		// Mapeo de píxel a plano complejo
		float px = ofMap(x, 0, imgWidth, -2.0f, 1.0f);
		float py = ofMap(y, 0, imgHeight, -1.5f, 1.5f);

		float zx, zy, cx, cy;
		if (useJulia) {
			// Julia: z = pixel, c = juliaK
			zx = px;
			zy = py;
			cx = juliaK.x;
			cy = juliaK.y;
		} else {
			// Mandelbrot: z = 0, c = pixel
			zx = 0.0f;
			zy = 0.0f;
			cx = px;
			cy = py;
		}

		int iterations = 0;
		while (zx * zx + zy * zy < 4.0f && iterations < maxIterations) {
			float tmp = zx * zx - zy * zy + cx;
			zy = 2.0f * zx * zy + cy;
			zx = tmp;
			iterations++;
		}
		return iterations;
	}

	ofColor mapIterationsToColor(int iterations) {
		if (iterations == maxIterations) return ofColor::black;
		float hue = ofMap(iterations, 0, maxIterations, 0, 255);
		float brightness = ofMap(iterations, 0, maxIterations, 100, 255);
		float saturation = 200;
		return ofColor::fromHsb(hue, saturation, brightness);
	}
};

// -----------------------------
// ofApp
// -----------------------------
class ofApp : public ofBaseApp {

public:
	void setup();
	void update();
	void draw();
	void exit();
	void keyPressed(int key);
	void mouseMoved(int x, int y);

	void startCalculation();

	ofPixels pixels;
	ofTexture texture;

	int imgWidth;
	int imgHeight;
	int maxIterations;
	int numThreads;

	std::vector<MandelbrotThread *> threads;

	float startTime;
	float calculationTime;
	bool calculating;
	std::string statusMessage;
	int runningThreads;

	// Julia control
	ofVec2f juliaK;
	bool useJulia;
};
```
Codigo ofApp.cpp:
```c++
#include "ofApp.h"
#include <sstream>

//--------------------------------------------------------------
void ofApp::setup() {
	ofSetWindowTitle("Mandelbrot / Julia Paralelo (ofThread)");
	ofSetFrameRate(60);
	ofBackground(30);

	imgWidth = ofGetWidth();
	imgHeight = ofGetHeight();
	maxIterations = 100;

	numThreads = std::thread::hardware_concurrency();
	if (numThreads == 0) numThreads = 4;
	ofLogNotice() << "Usando " << numThreads << " hilos.";

	pixels.allocate(imgWidth, imgHeight, OF_PIXELS_RGB);
	texture.allocate(pixels);

	calculating = false;
	calculationTime = 0.0f;
	runningThreads = 0;
	statusMessage = "Listo. \nPresiona ESPACIO para calcular.";

	// Julia defaults
	juliaK.set(0.285f, 0.01f);
	useJulia = true; // comienza en Julia, pulsa 'j' para alternar
}

//--------------------------------------------------------------
void ofApp::startCalculation() {
	if (calculating) {
		ofLogWarning() << "Ya se está calculando, espera a que termine.";
		return;
	}

	calculating = true;
	runningThreads = 0;
	statusMessage = std::string("Calculando con ") + ofToString(numThreads) + " hilos...";

	ofLogNotice() << statusMessage;
	startTime = ofGetElapsedTimef();

	// Limpiar hilos previos si existen
	if (!threads.empty()) {
		ofLogVerbose() << "Limpiando hilos anteriores...";
		for (auto & t : threads) {
			t->waitForThread(true);
			delete t;
		}
		threads.clear();
		ofLogVerbose() << "Hilos anteriores limpiados.";
	}

	int rowsPerThread = imgHeight / numThreads;
	for (int i = 0; i < numThreads; ++i) {
		int startY = i * rowsPerThread;
		int endY = (i == numThreads - 1) ? imgHeight : (i + 1) * rowsPerThread;

		MandelbrotThread * newThread = new MandelbrotThread(startY, endY, imgWidth, imgHeight, maxIterations, pixels, juliaK, useJulia);
		threads.push_back(newThread);
		runningThreads++;
		threads.back()->startThread();
		ofLogVerbose() << "Lanzado hilo " << i << " para filas " << startY << "-" << endY;
	}
	ofLogNotice() << runningThreads << " hilos lanzados.";
}

//--------------------------------------------------------------
void ofApp::update() {
	bool allThreadsFinished = true;
	if (!threads.empty()) {
		for (const auto & t : threads) {
			if (t->isThreadRunning()) {
				allThreadsFinished = false;
				break;
			}
		}
	} else {
		allThreadsFinished = true;
	}

	if (allThreadsFinished && calculating) {
		calculationTime = ofGetElapsedTimef() - startTime;
		calculating = false;
		runningThreads = 0;
		statusMessage = "Cálculo completado. \nPresiona ESPACIO para recalcular.";
		ofLogNotice() << statusMessage << " Tiempo: " << calculationTime << " s";
		texture.loadData(pixels);
	}
}

//--------------------------------------------------------------
void ofApp::draw() {
	ofSetColor(255);
	texture.draw(0, 0, ofGetWidth(), ofGetHeight());

	std::stringstream ss;
	ss << (useJulia ? "Modo: Julia" : "Modo: Mandelbrot") << std::endl;
	ss << "Status: " << statusMessage << std::endl;
	if (!calculating && calculationTime > 0.0f) {
		ss << "Ultimo Tiempo: " << ofToString(calculationTime, 3) << " s" << std::endl;
	}
	ss << "Hilos Usados: " << numThreads << std::endl;
	ss << "Max Iteraciones: " << maxIterations << std::endl;
	ss << "Resolucion: " << imgWidth << "x" << imgHeight << std::endl;
	ss << "FPS: " << ofToString(ofGetFrameRate(), 0) << std::endl;
	if (useJulia) {
		ss << "Julia k: (" << ofToString(juliaK.x, 3) << ", " << ofToString(juliaK.y, 3) << ")" << std::endl;
		ss << "Mueve el raton para cambiar k (recalculado automaticamente)";
	} else {
		ss << "Pulsa 'j' para cambiar a Julia (mouse activo)";
	}

	ofSetColor(0, 180);
	ofDrawRectangle(10, 10, 380, 140);
	ofSetColor(255);
	ofDrawBitmapString(ss.str(), 20, 30);
}

//--------------------------------------------------------------
void ofApp::exit() {
	ofLogNotice() << "Saliendo, esperando a los hilos...";
	for (auto & t : threads) {
		if (t) {
			t->waitForThread(true);
			delete t;
		}
	}
	threads.clear();
	ofLogNotice() << "Hilos detenidos y limpiados. Adiós.";
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
	if (key == ' ') {
		maxIterations += 1;
		startCalculation();
	}
	if (key == 'n') {
		maxIterations = 0;
		startCalculation();
	}
	if (key == 'j' || key == 'J') {
		useJulia = !useJulia;
		startCalculation();
	}
}

//--------------------------------------------------------------
void ofApp::mouseMoved(int x, int y) {
	// Mapear mouse a rango -1.5 .. 1.5
	juliaK.x = ofMap(x, 0, ofGetWidth(), -1.5f, 1.5f);
	juliaK.y = ofMap(y, 0, ofGetHeight(), -1.5f, 1.5f);

	// Si estamos en modo Julia, recalcular con la nueva k
	if (useJulia) startCalculation();
}
```

### AutoEvaluacion

Mi nota es un 4, ya que realice 4 actividades y realice el apply. 

*Como nota adicional me gustaria decir que me gusto mucho como se maneja el curso y las falencias que le demuestran a uno, tanto en respondabilidad, no procrastinar los trabajos y el manejo del tiempo; me quedan muchas cosas que aprender como tal de la materia pero tambien como estudiante, es decir, esta materia me dejo saber que aveces mi sistema de estudio no es el mas eficiente y que cursos anteriores me han dejado con algunos vacios a los cuales no he prestado atencion. En general me gusto mucho haber tenido esta clase contigo y me alegra decir que eres uno de esos profes que daria gusto volver a ver durante la carrera, muchas gracias por todo 🩷.*







