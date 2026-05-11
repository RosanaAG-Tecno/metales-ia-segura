# Laboratorio de metales con IA segura

Este proyecto convierte la web de ensayos mecánicos en una versión preparada para IA segura.

## Estructura

- `index.html`: web para GitHub Pages. No contiene claves API.
- `api/chat-metales.js`: función serverless para Vercel. Aquí se llama a la IA desde el servidor.
- `.env.example`: ejemplo de variables de entorno.
- `vercel.json`: configuración mínima para desplegar el backend.

## Funcionamiento

La web puede funcionar de dos formas:

1. **Modo local sin IA**: usa el chatbot didáctico basado en reglas. Funciona sin conexión y sin backend.
2. **Modo IA segura**: el `index.html` llama a un backend en Vercel. La clave de OpenAI está solo en Vercel y nunca aparece en GitHub.

El backend aplica estas medidas:

- Filtra preguntas fuera del tema.
- Usa moderación.
- Selecciona solo fuentes aprobadas por la profesora.
- Pide a la IA que responda únicamente con ese contexto.
- Devuelve las fuentes usadas junto con la respuesta.

## Paso 1. Subir la web a GitHub Pages

Sube `index.html` al repositorio de GitHub que usarás para la web.

Puedes probarla sin IA: seguirá funcionando con el chatbot local.

## Paso 2. Crear el backend en Vercel

1. Crea una cuenta en Vercel o entra con GitHub.
2. Crea un nuevo proyecto y sube esta carpeta completa.
3. En **Settings → Environment Variables**, añade:

```text
OPENAI_API_KEY=tu_clave_api
OPENAI_MODEL=gpt-5.5-mini
OPENAI_MODERATION_MODEL=omni-moderation-latest
ALLOWED_ORIGIN=https://TU-USUARIO.github.io
```

Si el modelo indicado no está disponible en tu cuenta, cambia `OPENAI_MODEL` por uno disponible.

## Paso 3. Conectar GitHub Pages con Vercel

Cuando Vercel te dé la URL del proyecto, edita esta línea en `index.html`:

```html
window.METALES_AI_BACKEND = "https://TU-PROYECTO.vercel.app/api/chat-metales";
```

Está al principio del bloque `<script>`.

No pongas nunca `OPENAI_API_KEY` en el HTML.

## Paso 4. Añadir más fuentes fiables

Edita el array `APPROVED_SOURCES` dentro de `api/chat-metales.js`.

Cada fuente tiene esta estructura:

```js
{
  id: 'nombre-corto',
  title: 'Título visible',
  url: 'https://...',
  tags: ['traccion', 'dureza', 'charpy'],
  content: 'Resumen validado por la profesora. La IA solo podrá usar esta información.'
}
```

Es mejor añadir resúmenes validados que permitir búsqueda libre en internet.

## Recomendación didáctica

Pide al alumnado que formule preguntas con esta estructura:

```text
Tengo una pieza que debe cumplir esta función...
El fallo que quiero evitar es...
¿Qué propiedad debería analizar y qué ensayo usaría?
```

Así el chatbot devuelve una respuesta competencial: función → fallo → propiedad → ensayo → conclusión.
