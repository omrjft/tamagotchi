# Agentes de Desarrollo: Proyecto Tamagotchi Web

Para asegurar una ejecución eficiente del `PLAN.md`, el trabajo de desarrollo se dividirá entre los siguientes agentes especializados. Cada agente debe enfocarse en su dominio y colaborar para integrar el código en un único archivo web.

## 1. Agente de Interfaz y Experiencia de Usuario (Frontend UI/UX)
**Rol:** Diseñador y Maquetador Web.
**Responsabilidades:**
*   **Estructura Base:** Crear el esqueleto HTML (pantalla de inicio, pantalla principal del juego y modal de resumen final).
*   **Estilos y Animaciones:** Aplicar CSS (o frameworks como Tailwind) para asegurar que el Tamagotchi tenga un aspecto atractivo y amigable.
*   **Componentes Visuales:**
    *   Diseñar el reloj digital.
    *   Crear los indicadores visuales (barras de progreso o texto) para Hambre, Diversión, Higiene y Felicidad.
    *   Estilizar los botones de acción (Alimentar, Jugar, Baño).
    *   Crear el contenedor de mensajes (bocadillo de diálogo del avatar).
*   **Estados del Avatar:** Asegurar que el avatar cambie visualmente (ej. de un emoji feliz `🐶` a un fantasma `👻` cuando muera).

## 2. Agente de Lógica de Juego (Game Engine Developer)
**Rol:** Desarrollador JavaScript Core.
**Responsabilidades:**
*   **Motor de Tiempo:** Implementar el `setInterval` principal donde 6 segundos de la vida real equivalen a 1 hora simulada. Detener el ciclo a las 24 horas simuladas.
*   **Gestión de Estado:** Manejar las variables internas de la mascota (nivel de hambre, higiene, diversión).
*   **Sistema de Reglas (Muerte):**
    *   Programar la lógica que cuenta las solicitudes de hambre ignoradas (2 = muerte por inanición).
    *   Programar la lógica que cuenta la comida excesiva (3 veces sin pedir = muerte por empacho).
*   **Eventos Aleatorios:** Crear el generador de números aleatorios que dispare las necesidades de ir al baño o jugar.
*   **Interacciones:** Conectar la lógica con los botones de la interfaz para que las estadísticas se actualicen cuando el usuario interactúe.

## 3. Agente de Control de Calidad (QA & Tester)
**Rol:** Evaluador de Condiciones y Flujos.
**Responsabilidades:**
*   **Validación de Tiempo:** Verificar que el reloj del juego esté sincronizado exactamente con la escala de 6s reales = 1h simulada.
*   **Casos de Prueba (Edge Cases):**
    *   *Caso A (Inanición):* Simular no dar comida durante 12 horas simuladas para verificar que se convierta en fantasma exactamente al 2do aviso ignorado.
    *   *Caso B (Empacho):* Simular hacer clic compulsivamente en "Alimentar" para verificar la muerte por exceso.
    *   *Caso C (Victoria):* Simular un cuidado perfecto durante 144 segundos reales para verificar que se muestra el resumen final correctamente.
*   **Feedback de UX:** Asegurar que los mensajes del avatar correspondan correctamente al estado actual de las variables (ej. que no diga que tiene hambre si acaba de comer).