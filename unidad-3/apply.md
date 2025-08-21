# Unidad 3


## 🛠 Fase: Apply

### Actividad Integradora
#### 1. Diagnostico del problema (analisis)
- Falta de metodo destructor.
  Ocurre ya que el personaje guarda las caracteristicas en el heap, y como no existe un metodo destructor, el int[3] no se libera, entonces sigue y sigue y sigue creando NPC's que al terminar el programa no se borran, consumiendo muchisima RAM.  
  Codigo que arregla ese error:
 ```c++
 ~Personaje()
    {
        delete[] estadisticas;
        std::cout << "Destructor: muere " << nombre << std::endl;
    }
```


