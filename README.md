
# TP Integrador - "BlackJack"

Trabajo práctico integrador para las materias Laboratorio de Computación IV y Metodología de Sistemas I, de curso en la UTN Mar del Plata en el año 2023.

Diseñado e implementado en JavaScript/Angular, con uso de la API "Deck of Cards" hecha por Chase Roberts ([@crobertsbmw](https://github.com/crobertsbmw/)).



[INFO. A CONTINUACIÓN SUJETA A CAMBIOS]

En este proyecto se diseñó un juego de Blackjack, tal cual el juego original de cartas que se puede jugar en casinos.

Inicialmente se implementará un juego de un único jugador contra el croupier, siendo lo ideal poder sumar más jugadores en la misma mesa de ser deseado.

Se juega contra el croupier, en representación de la "casa" (casino), que seguirá las reglas fijas en base a decisiones muy básicas (if/else).

El bucle de juego, generalmente, se basa en 6 barajas de cartas inglesas mezcladas, sin comodines. Esto permite que se repitan cartas con relativa constancia. Llegar a un reinicio de bucle (quedarse sin cartas) llevaría mucho tiempo, por lo tanto se añadirá un botón para simularlo y apreciar la funcionalidad. El reinicio es básicamente mezclar los 6 mazos nuevamente y continuar.

Se podrán crear usuarios, al hacerlo se les regalará 100 fichas iniciales. Los jugadores podrán recargar fichas desde su perfil o si llegan a quedarse sin fichas para la apuesta que estén tratando de hacer en el juego. Se implementará una simulación de pago digital para tal fin. Si llegan a 0 fichas cuando estén jugando, se les pedirá que elijan entre recargar fichas en el acto o abandonar la mesa. Si se diera la situación que todos los jugadores abandonen la mesa, se cerrará el juego, se volverán a mezclar las cartas y se volverá al lobby de la aplicación.
## Autores

- Codeado, diseñado, etc. por Tomás Agüero Pizzi
- GitHub: [@PonFET](https://www.github.com/PonFET)


## API Deck of Cards (https://deckofcardsapi.com)

Solamente se listarán los comandos a usar en el proyecto. Varias funciones interesantes de la API no funcionan cuando se tienen múltiples mazos juntos, como por ejemplo las pilas de cartas, pero se diseñarán dentro del juego con código propio.

###

#### Mezclar cartas y elegir cantidad de mazos

```http
  https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1
```

| Parámetero | Descripción                |
| :-------- | :------------------------- |
| `deck_count` | **Opcional**. Usarlo en GET o POST para definir la cantidad de mazos a usar. Por defecto se usa 1.  |

### Barajar una carta

```http
  https://deckofcardsapi.com/api/deck/<<deck_id>>/draw/?count=2
```

| Parámetero | Descripción                |
| :-------- | :------------------------- |
| `deck_id` | Cambiar por un ID válido. La API crea mazos únicos para identificar quién los usa y los descarta a las dos semanas de no usarlos. |
| `count` | Cantidad de cartas a barajar en un sólo llamado. |

### Mezclar barajas

```http
https://deckofcardsapi.com/api/deck/<<deck_id>>/shuffle/
https://deckofcardsapi.com/api/deck/<<deck_id>>/shuffle/?remaining=true
```

Las barajas se pueden reutilizar para volver a jugar siempre que no se haya descartado el ID único.

| Parámetero | Descripción                |
| :-------- | :------------------------- |
| `deck_id` | Cambiar por un ID válido. La API crea mazos únicos para identificar quién los usa y los descarta a las dos semanas de no usarlos. |
| `remaining=true` | Usar para especificar que se quieren mezclar únicamente las cartas que quedan en el mazo. No usarlo da por entendido que se mezclan todas las cartas, incluso las ya jugadas. |

### Abrir nuevo mazo

```http
https://deckofcardsapi.com/api/deck/new/
```
Abre un mazo nuevo, tal cual vendría en una caja: En orden numérico ascendente, empezando por Picas, y siguiendo con Diamantes, Tréboles, y finalmente Corazones.

| Parámetero | Descripción                |
| :-------- | :------------------------- |
| `jokers_enabled=true` | **Opcional**. Usarlo en GET o POST para especificar que haya dos comodines en el mazo __(no se usará en este proyecto)__.  |

### Devolver cartas al mazo

```http
https://deckofcardsapi.com/api/deck/<<deck_id>>/return/
```
Devuelve todas las cartas barajadas al mazo.
| Parámetero | Descripción                |
| :-------- | :------------------------- |
| `deck_id` | Cambiar por un ID válido. La API crea mazos únicos para identificar quién los usa y los descarta a las dos semanas de no usarlos. |

### Link al reverso de las cartas

```http
https://deckofcardsapi.com/static/img/back.png
```

