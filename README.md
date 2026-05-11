# Laboratorio de metales con IA segura en Netlify

Este proyecto publica la web y la función de IA segura en Netlify.

## Estructura

- `index.html`: web educativa.
- `netlify/functions/chat-metales.js`: función segura que llama a OpenAI desde el servidor.
- `netlify.toml`: configuración de Netlify.
- `.env.example`: ejemplo de variables. No contiene claves reales.

## Funcionamiento

La web llama a:

```text
/.netlify/functions/chat-metales
```

La clave `OPENAI_API_KEY` se guarda en Netlify como variable de entorno y no aparece en el HTML.

## Variables necesarias en Netlify

```text
OPENAI_API_KEY=tu_clave_real
OPENAI_MODEL=gpt-4o-mini
OPENAI_MODERATION_MODEL=omni-moderation-latest
ALLOWED_ORIGIN=*
```

Cuando todo funcione, puedes sustituir `ALLOWED_ORIGIN=*` por la URL de tu web de Netlify.
