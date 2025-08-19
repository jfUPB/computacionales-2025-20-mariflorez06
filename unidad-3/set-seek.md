# Unidad 3

## 🔎 Fase: Set + Seek
### Notas
- Actividad 1:
  
 ¿Para qué sirven los breakpoints?

= Para detener la depuración (detener el programa). 

¿Para qué se usa la ventana de depuración Autos?  

= Todas las variables locales que se van definiendo con el pasar del programa
- Actividad 2:
 ```c++
void swapPorValor(int a, int b) {
    cout << "Dentro de swapPorValor. a,b: " << a << ","<< b << endl;
    int tmp = b;
    b = a;
    a = tmp;
    cout << "Dentro de swapPorValor, valor modificado: a " << a << "y b:" <<b<<endl;

cout << "\nLlamando a swapPorValor..." << endl;
swapPorValor(a,b);
cout << "Después de swapPorValor, valor de a,b: " << a << ","<<b<<endl;
```
- Actuvidad 3:
  
Las variables estáticas se inicializa una sola vez, si luego tiene un ++ se incrementa, en cambio, las variables no estáticas se inicializa cada que se llama la función, si luego tiene un ++ no se incrementará.
  
  


