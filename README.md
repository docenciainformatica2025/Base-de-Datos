# Base-de-Datos

Pequeña aplicación de cuestionarios (Next.js) para evaluar conocimientos. Incluye un componente cliente `Test_BD` que maneja el flujo del examen: carga de información del estudiante, despliegue de preguntas, progreso, pistas y persistencia de resultados en localStorage.

## Requisitos
- Entorno: contenedor de desarrollo (Ubuntu 24.04.2 LTS).
- Node.js y gestor de paquetes (npm / yarn / pnpm) instalados en el contenedor.
- Para abrir una URL en el navegador del host desde este entorno, use:
    "$BROWSER" <url>

## Cómo ejecutar (desarrollo)
1. Instale dependencias:
     - npm: `npm install`
     - yarn: `yarn`
     - pnpm: `pnpm install`
2. Inicie en modo desarrollo:
     - npm: `npm run dev`
3. Abra la app en el navegador (por ejemplo): `"$BROWSER" http://localhost:3000`

## Comportamiento relevante
- El componente cliente `Test_BD`:
    - Verifica que exista `studentInfo` en localStorage; si no, redirige a la página inicial.
    - Baraja las preguntas una sola vez al montar el componente.
    - Al finalizar calcula la puntuación, crea un objeto `StudentResult` con un `id` (timestamp) y guarda:
        - Historial en `quizResults` (array)
        - Resultado actual en `currentResult`
- Claves de localStorage usadas:
    - `studentInfo` — datos del estudiante (JSON)
    - `quizResults` — historial de resultados (array JSON)
    - `currentResult` — último resultado (JSON)

## Archivos y módulos relevantes
- `@/lib/quiz-data` — datos de las preguntas.
- `@/lib/types` — tipos: Question, StudentInfo, AnswerRecord, StudentResult.
- `@/components/ui/*` — componentes UI reutilizables usados por `Test_BD`.
- Componente principal relacionado: `Test_BD` (componente cliente que contiene la lógica del examen).

## Reset de datos
- Para borrar los resultados o la información del estudiante desde el navegador:
    - Usar DevTools → Application → Local Storage → eliminar las claves mencionadas, o ejecutar en consola:
        - `localStorage.removeItem('studentInfo')`
        - `localStorage.removeItem('quizResults')`
        - `localStorage.removeItem('currentResult')`

## Build / Producción
- Build: `npm run build`
- Start: `npm start` (o según la configuración del proyecto Next.js)

Contribuciones y mejoras (sugeridas):
- Persistencia en backend para guardar historial por usuario.
- Autenticación y gestión de usuarios.
- Mejorar accesibilidad y almacenamiento seguro de respuestas.
- Añadir tests unitarios/integación para la lógica de evaluación.Base-de-Datos