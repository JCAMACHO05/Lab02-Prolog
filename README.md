# Laboratorio 02 - Busquedas en Prolog  

## 📌 Descripción  
Este laboratorio tiene como objetivo que los estudiantes fortalezcan sus conocimientos relacionados a algoritmos de busqueda en **Prolog**.

El desarrollo se realizará en **[SWISH Prolog](https://swish.swi-prolog.org/)**, un entorno en línea que no requiere instalación local.  

---

## 🛠️ Instrucciones Generales  

1. **Fork del repositorio**  
   - Realice un **fork** de este repositorio en su cuenta personal de GitHub.  
   - No realice cambios directamente sobre el repositorio original.  

2. **Estructura de carpetas**  
   - Dentro de su fork, cree una carpeta llamada **`lab02/`**.  
   - Cada ejercicio debe resolverse en un archivo **independiente** con el siguiente formato:  
     ```
     lab02/ejercicio01.pl
     lab02/ejercicio02.pl
     ...
     ```  

3. **Resolución de ejercicios**  
   - Desarrolle los programas en **SWISH Prolog**.  
   - Una vez finalizados, copie el código a los archivos `.pl` correspondientes en su repositorio.  
   - Cada archivo debe contener:
     - La implementación de su solución.  

4. **Buenas prácticas**  
   - Use **nombres de predicados claros y significativos**.
---

## 🚀 Entrega  

- **Plazo**: La entrega debe realizarse a mas tardar el proximo lunes, se habilitara una tarea en Moodle para adjuntar el link del repositorio.

---

## ✅ Criterios de Evaluación  

1. **Correctitud de las soluciones** (funcionalidad de los predicados).  
2. **Cumplimiento de la estructura solicitada** (archivos independientes en `lab01/`).  
3. **Claridad en la codificación** (nombres, comentarios y legibilidad).  
4. **Uso adecuado de variables** (incluyendo variables anónimas donde corresponda).  

---

## 💡 Recomendaciones  

- Revise la documentación oficial de Prolog: [SWI-Prolog Documentation](https://www.swi-prolog.org/pldoc/).  
- Antes de subir sus archivos, **ejecute y verifique** cada consulta en SWISH.  
- Mantenga su repositorio organizado y actualizado.

---

## Ejercicio 1 - Problema de la rana

Un problema bien conocido es aquel de la rana donde dados un punto de inicio junto con otros puntos que representan la ubicación de una serie de piedras se quiere determinar si una rana la cual tiene
una capacidad maxima de salto puede llegar a un punto objetivo.

Para este problema se tienen los siguientes hechos.

```
% --- HECHOS Y CAPACIDADES (PARÁMETROS DEL PROBLEMA) ---

% Coordenadas de las ubicaciones: ubicacion(ID, X, Y).
ubicacion(orilla_inicial, 0, 5).
ubicacion(piedra1, 2, 4).
ubicacion(piedra2, 5, 6).
ubicacion(piedra3, 8, 4).
ubicacion(piedra4, 5, 0).
ubicacion(orilla_final, 10, 5).

% Capacidad de la rana: distancia máxima de salto.
salto_maximo(4.0).
```

Usando el algoritmo generico de DFS visto en clase, poder determinar si la rana puede llegar de la `orilla_inicial` a la `orilla_final`.

Definir la regla `siguiente_estado/2`, que determine si es posible pasar de un estado a otro, esta puede definirse así, donde consultado `ubicacion` para `LugarActual`, se obtienen las ubicaciones.

```
siguiente_estado(pos(LugarActual), pos(LugarSiguiente))
```

Asi se puede iniciar la busqueda en el espacio de soluciones.

```
buscar_solucion(Solucion) :-
    EstadoInicial = pos(orilla_inicial),
    dfs(EstadoInicial, [EstadoInicial], Solucion). %dfs(Estado,Visitados, Solucion)
```

---

## Ejercicio 2 - Problema de Batman vs Villanos

Se tiene un problema donde dados una lista de poderes y su respectivo daño, asi como el costo asociado a usar este, junto con una lista de villanos con sus puntos de vida, y una lista de sus debilidades a poderes.

Se quiere encontrar si batman es capaz de derrotarlos teniendo este una cantidad de energia que se agota al usar cada poder, asi como la condicion de que puede omitir el uso de un poder e intentar usar otro contra el mismo villano.

Para este problema se tienen los siguientes hechos.

Aqui se tiene por ejemplo el poder logica que hace 100 de daño, y usa 10 de energia, y se tiene el villano riddler que tiene 90 de salud y es debil a logica y sigilo.

```
power_list([
    power(logica, 100, 10),
    power(sigilo, 150, 30),
    power(fuerza, 250, 50)
]).

villain_list([
    villain(riddler, 90, [logica, sigilo]),
    villain(bane, 240, [fuerza])
]).
```

Usando el algoritmo DFS visto en clase, poder determinar si batman puede derrotar a todos los villanos con la energia disponible o no.

Asi se puede iniciar la busqueda en el espacio de soluciones.

```
batman_can_win(EnergiaMaxima) :-
    power_list(Superpoderes),
    villain_list(Villanos),
    % El estado inicial contiene todos los villanos, todos los poderes y la energía máxima.
    EstadoInicial = estado(Villanos, Superpoderes, EnergiaMaxima),
    dfs(EstadoInicial, [EstadoInicial]). %dfs(Estado,Visitados)
```

---

## Ejercicio 3 - 8 reinas

Se quiere resolver el problema de las [8 reinas](https://es.wikipedia.org/wiki/Problema_de_las_ocho_reinas) usanado DFS, donde un estado se puede entender como una lista donde cada elemento representa
la fila en la que esta esa reina, es decir [4,3] dice que en hay reinas en la columna 1, fila 4, y columna 2, fila 3.

Asi se puede definir la regla de dfs para solo tener en cuenta la solucion final y no todo el camino.

```
dfs(EstadoActual, Visitados, SolucionFinal)
```

Asi se puede iniciar la busqueda en el espacio de soluciones.

```
solucion(Solucion) :-
    EstadoInicial = [],
    dfs(EstadoInicial, [EstadoInicial], Solucion).
```

---


## Retrospectiva
1. ¿Cuál fue el tiempo total invertido en el laboratorio por cada uno de ustedes? (Horas/Hombre)
Mi tiempo invertido en el laboratorio fue de 1 hora y 58 minutos, lo que equivale aproximadamente a 1.97 horas/hombre.
2. ¿Cuál es el estado actual del laboratorio? ¿Por qué?
El laboratorio se encuentra finalizado y funcional, ya que se logró implementar correctamente el algoritmo solicitado utilizando DFS. El programa cumple con los requerimientos planteados, permite ejecutar las consultas sin errores y genera los resultados esperados.
3. ¿Cuál consideran fue el mayor logro? ¿Por qué?
El mayor logro fue modelar correctamente el problema como un espacio de estados y aplicar el algoritmo DFS de manera adecuada. Esto permitió comprender cómo representar estados, generar sucesores y definir correctamente el estado meta. Además, se logró evitar ciclos mediante el uso de la lista de visitados.
4. ¿Cuál consideran que fue el mayor problema técnico? ¿Qué hicieron para resolverlo?
El mayor problema técnico fue definir correctamente la regla siguiente_estado/2, especialmente al momento de manejar las condiciones del problema (como restricciones o validaciones).

Para solucionarlo, se revisó paso a paso la lógica del estado, se probaron consultas intermedias en Prolog y se realizaron ajustes hasta asegurar que la generación de sucesores fuera correcta y consistente.

5. ¿Qué hicieron bien como equipo? ¿Qué se comprometen a hacer para mejorar los resultados?
Como equipo, trabajamos bien en la distribución de tareas y verificación del código, asegurándonos de que cada parte del algoritmo funcionara correctamente antes de integrarlo.

Nos comprometemos a mejorar en la planificación del tiempo y en la documentación del código, para facilitar futuras revisiones y hacer más eficiente el proceso de desarrollo.
6. ¿Qué referencias usaron? ¿Cuál fue la más útil? Incluyan citas con estándares adecuados.
Se utilizaron las siguientes referencias:
	•	Russell, S., & Norvig, P. (2021). Artificial Intelligence: A Modern Approach (4th ed.). Pearson.
	•	Bratko, I. (2012). Prolog Programming for Artificial Intelligence (4th ed.). Addison-Wesley.
	•	Material de clase y diapositivas del curso.

La referencia más útil fue Russell & Norvig (2021), ya que explica de manera clara el algoritmo de búsqueda en profundidad (DFS) y su aplicación en problemas de espacio de estados.


