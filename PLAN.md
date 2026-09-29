# Plan de Desarrollo: Mascota Tamagotchi Web (Simulador de 1 Día)

Este documento es una guía paso a paso para construir un simulador web de una mascota virtual (tipo Tamagotchi) que dura exactamente 24 horas simuladas. 

## 1. Configuración Inicial e Interfaz de Usuario (UI)
*   **Pantalla de Inicio:** 
    *   Crear un formulario modal o pantalla inicial que pida al usuario el nombre de la mascota.
    *   Un botón de "Comenzar" que oculte esta pantalla y revele el juego.
*   **Pantalla Principal (Juego):**
    *   **Cabecera:** Mostrar el nombre de la mascota y un Reloj Digital (empezando en 00:00 o la hora 1).
    *   **Área del Avatar:** Un div central donde se mostrará la mascota (puede ser un emoji o CSS art simple) y los mensajes de estado (ej. globos de diálogo).
    *   **Panel de Estadísticas (Barras o Porcentajes):**
        *   Hambre (0-100%)
        *   Diversión (0-100%)
        *   Higiene (0-100%)
        *   Felicidad general (Promedio de las tres anteriores).
    *   **Panel de Controles (Botones):**
        *   🍕 Alimentar
        *   🎾 Jugar
        *   🚽 Llevar al Baño

## 2. Motor de Tiempo (Game Loop)
*   **Reloj Simulado:**
    *   Implementar un `setInterval`.
    *   **Escala de tiempo:** 6 segundos de tiempo real = 1 hora en el juego.
    *   El ciclo total del juego será de 144 segundos reales (24 horas simuladas).
    *   Actualizar el reloj en la interfaz cada vez que pase una hora simulada.
*   **Condición de Fin de Día:**
    *   Al llegar a la hora 24 (o al pasar 144 segundos), detener todos los temporizadores y llamar a la función de Fin de Juego (Resumen).

## 3. Lógica de Estados y Necesidades (Hambre y Fantasma)
*   **Ciclo de Hambre:**
    *   Cada 6 horas simuladas (36 segundos reales), el sistema dispara el evento "Tengo Hambre".
    *   El indicador de hambre debe bajar drásticamente en este punto.
*   **Condiciones de Muerte (Transformación en Fantasma 👻):**
    *   *Inanición:* Llevar un contador de `solicitudes_hambre_ignoradas`. Si la mascota pide comida 2 veces seguidas y no se le da a través del botón, transformar el avatar en fantasma `👻`, mostrar mensaje de derrota y detener el juego.
    *   *Sobrecrecimiento/Empacho:* Llevar un contador de `comida_excesiva`. Si el usuario presiona el botón de alimentar 3 veces cuando la mascota NO lo ha solicitado (o ya está llena), transformarla en fantasma, mostrar mensaje de derrota y detener el juego.

## 4. Eventos Aleatorios
*   **Lógica de Randomización:**
    *   En cada "hora simulada" (excepto en las horas fijas de hambre), generar un número aleatorio para determinar si ocurre un evento.
*   **Tipos de Eventos:**
    *   *Quiere Jugar:* Baja la estadística de Diversión. La mascota lanza un mensaje: "¡Estoy aburrido! Juega conmigo".
    *   *Necesita ir al baño:* Baja la estadística de Higiene. Mensaje: "¡Me hago pipí!".
*   *Nota:* Estos eventos no matan a la mascota directamente, pero reducen la "Felicidad" general si son ignorados y afectan el puntaje final.

## 5. Acciones del Usuario (Botones)
*   **Alimentar:** Restaura el nivel de Hambre. Reinicia el contador de hambre actual. (Validar la regla del empacho aquí).
*   **Jugar:** Restaura el nivel de Diversión y muestra un mensaje feliz.
*   **Llevar al Baño:** Restaura el nivel de Higiene y limpia cualquier mensaje de suciedad.

## 6. Sistema de Mensajes y Feedback
*   Implementar una caja de texto o un "bocadillo de cómic" sobre la mascota.
*   Mostrar actualizaciones de texto según las acciones:
    *   "¡Ñam ñam! Qué rico."
    *   "¡Weee! Me encanta jugar."
    *   "Uff, qué alivio."
    *   "Tengo mucha hambre..."

## 7. Fin del Juego y Resumen
*   Al completarse el ciclo de 24 horas (sin haberse convertido en fantasma), ocultar la interfaz principal de controles.
*   Mostrar un Modal de **Resumen de Cuidado**:
    *   Felicitar al usuario.
    *   Mostrar el promedio final de Felicidad, Higiene y Diversión.
    *   Clasificar el desempeño (ej. "Excelente Cuidador", "Cuidador Decente", "De milagro sobrevivió").
    *   Botón para "Jugar de Nuevo" (reinicia el estado global).