## Descripción:

¡Aprende a sumar a base de golpes! Un divertido juego de acción para Android donde la agilidad mental y tus reflejos son la clave. Resuelve el objetivo matemático oculto estallando los globos correctos antes de que te quedes sin vidas. Esquiva los globos trampa, supera las oleadas cada vez más rápidas y conviértete en un auténtico Suma Ninja.

## Funcionalidades:

*   **Matemáticas Dinámicas:** sumas básicas adaptadas a niños de infantil. El resultado está oculto, por lo que el jugador debe realizar el cálculo mental para saber qué globos estallar.
*   **Dificultad Progresiva:** A medida que el jugador acierta sumas, la velocidad y la frecuencia de aparición de los globos aumenta gracias a un multiplicador interno.
*   **Ataques Direccionales:** Posibilidad de jugar en cooperativo, con ataques normales, agachados o saltando.
*   **Sistema de Vidas:** 3 vidas. El jugador pierde una vida si el valor acumulado sobrepasa el objetivo matemático o si baja de cero por comerse globos trampa rojos.
*   **Sistema de Audio Completo:**

## Arquitectura del Proyecto

El juego está desarrollado nativamente para Android utilizando Kotlin. En lugar de apoyarse en las vistas clásicas de Android o en motores pesados como Unity, el juego dibuja los gráficos de forma nativa utilizando un **Canvas 2D** acelerado por hardware a través de un **Game Loop** personalizado impulsado por **Corrutinas de Kotlin**. Esto garantiza un rendimiento suave 60 FPS manteniendo el peso de la aplicación extremadamente bajo.

---

## Patrones de Diseño Utilizados

1.  **State Pattern:** Se utiliza en el paquete de entidades. El personaje puede transicionar de forma segura y encapsulada entre estados, facilitando la lógica de animación y físicas sin recurrir a gigantescos bloques `if/else` anidados.
2.  **Singleton Pattern:** Clases globales que manejan los sprites, los sonidos y las mecánicas de la ronda.
3.  **Dependency Injection:** Se emplea el inyector de dependencias ligero para distribuir las instancias Singleton y las Factories por toda la aplicación, manteniendo el código altamente desacoplado.
4.  **Game Loop Pattern:** El corazón del juego, que cuenta con un ciclo infinito estructurado en dos pasos continuos: para procesar lógicas y físicas y para repintar el Canvas.

---

## Estructura de Paquetes

La base de código está modularizada para ser escalable:
    *   `Config.kt`: Constantes del juego físicas, velocidades, tamaños de pantalla.
    *   `GameView.kt`: Superficie personalizada de dibujado Canvas y HUD.
    *   `SoundManager.kt` / `SpriteManager.kt`: Gestores de carga y caché de memoria.
*   `com.mijuego.di`:
    *   `GameModule.kt`: Configuración de inyección de dependencias Koin.
*   `com.mijuego.entities`: Todos los objetos "vivos" del juego.
    *   `Character.kt` y `CharacterState.kt`: Físicas y lógica del jugador.
    *   `Balloon.kt`: Entidad individual del globo.
    *   `GameSession.kt`: El cerebro matemático que controla puntuaciones, multiplicadores y vidas.
*   `com.mijuego.input`:
    *   `InputManager.kt`: Gestor unificado para leer toques de pantalla o teclados externos.
*   `com.mijuego`: 
    *   `GameActivity.kt`: Actividad principal, orquestadora del bucle de vida de Android y del Game Loop.
       
---  

## Estructura

└───app\
    └───src\
        └───main\
            ├───res\
            │   ├───layout\
            │   ├───raw\
            │   └───values\
            │
            └───kotlin\
                └───com\
                    └───mijuego\
                        │   GameActivity.kt
                        │
                        ├───core\
                        │       Config.kt
                        │       GameView.kt
                        │       SoundManager.kt
                        │       SpriteManager.kt
                        │
                        ├───di\
                        │       GameModule.kt
                        │
                        ├───entities\
                        │       Balloon.kt
                        │       Character.kt
                        │       CharacterState.kt
                        │       GameSession.kt
                        │
                        └───input\
                                InputManager.kt

---

## Capturas

<img width="268" height="567" alt="interfaz" src="https://github.com/user-attachments/assets/ce9f15b1-a596-41a8-b4ff-1587599a004b" />

