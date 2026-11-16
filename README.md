# Recomendación de partidos abiertos con grafos ponderados

Presentación del **Grupo A²** para **Algoritmos y Estructuras de Datos 3**, Tecnicatura en Análisis de Sistemas.

**Integrantes:** Agustín Ramírez y Agustín Díaz

**Caso de aplicación:** AlquiPadel, plataforma de alquiler de canchas de pádel.

🔗 **Ver la presentación:** presentacion-grafos-alquipadel.html

## ¿De qué trata?

En AlquiPadel hay partidos abiertos que necesitan jugadores para completarse. Este proyecto propone un sistema de recomendación basado en un **grafo bipartito ponderado** que le sugiere a cada jugador los partidos que mejor le calzan según su **categoría** y su **localidad**.

## Cómo funciona el modelo

- **Nodos:** jugadores y partidos abiertos.
- **Aristas:** unen un jugador con un partido. Nunca unen jugador con jugador.
- **Peso:** un número de 0 a 1 que indica qué tan compatibles son.

```
peso = 0.6 × score_categoría + 0.4 × score_localidad
```

| Categoría | Score | Localidad | Score |
|---|---|---|---|
| Misma | 1.0 | Misma | 1.0 |
| Difiere en 1 nivel | 0.5 | Vecina | 0.5 |
| Difiere en 2 o más | 0 | Otra | 0 |

Para **recomendar**, se ordenan las aristas de un jugador por peso, de mayor a menor, y se toman las primeras.

## Implementación

- Representación: **lista de adyacencia** con un `Map` de JavaScript.
- Clase principal: `GrafoPonderado` (`agregarNodo`, `agregarArista`, `vecinos`).
- Funciones: `scoreCategoria`, `scoreLocalidad`, `calcularPeso`, `construirGrafo` y `recomendar`.

## Complejidad

| Operación | Costo |
|---|---|
| Construir el grafo (J jugadores, P partidos) | O(J × P) |
| Agregar una arista | O(1) |
| Recomendar (k aristas del jugador) | O(k log k) |
| Espacio con lista de adyacencia | O(J + A) |

## Contenido de la presentación

1. Portada
2. El problema
3. ¿Por qué grafos?
4. El modelo (grafo interactivo)
5. Cálculo del peso
6. Implementación: el grafo
7. Implementación: pesos y recomendación
8. Demo en vivo
9. Complejidad
10. Posibles mejoras
11. Conclusiones

## Estructura del repositorio

```
├── index.html   # La presentación completa (diapositivas, estilos y código)
└── README.md    # Este archivo
```

## Cómo ejecutarla

1. Descargá o cloná el repositorio.
2. Abrí `index.html` con doble clic en el navegador.

Necesita conexión a internet porque **Reveal.js** y las fuentes se cargan desde un CDN.

**Teclas útiles:**

- `←` `→` o las flechas de la esquina inferior derecha: cambiar de diapositiva.
- `F`: pantalla completa.
- `Esc`: ver todas las diapositivas.

## Cómo personalizar los datos

Dentro del bloque `<script>` de `index.html` están los datos de ejemplo:

- `PARTIDOS`: lista de partidos abiertos (id, categoría, localidad y horario).
- `VECINAS`: qué localidades se consideran vecinas entre sí.
- `JUG_EJ`: los tres jugadores que se dibujan en el grafo del modelo.

Reemplazalos por los datos reales de AlquiPadel.

## Tecnologías

- HTML, CSS y JavaScript
- [Reveal.js](https://revealjs.com/) 5.1.0
- SVG para el dibujo del grafo

## Posibles mejoras

- Sumar criterios al peso: horario, historial y nivel de los otros jugadores.
- Recorrer jugador → partido → jugador (BFS) para sugerir gente con quien ya jugaste.
- Usar Dijkstra con costo = 1 − peso para buscar conexiones indirectas.
- Evitar el recorrido J × P calculando solo contra partidos de la misma localidad y vecinas.

## Autores

**Grupo A²**: Agustín Ramírez y Agustín Díaz
