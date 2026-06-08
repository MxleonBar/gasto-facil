# Despliegue en Netlify

Este proyecto está completamente listo para publicarse en Netlify como una PWA sin servidor.

## Estructura del Proyecto

- **`public/`** - Frontend PWA estático (HTML, CSS, JavaScript)
- **`netlify/functions/`** - Backend serverless (funciones de Node.js)
- **`netlify.toml`** - Configuración de Netlify

## Pasos para Desplegar

### 1. Preparar Variables de Entorno

En Netlify, ve a **Site Settings → Environment → Environment Variables** y añade:

```
SUPABASE_URL = https://oeynlmlijfaqmqcxbchm.supabase.co
SUPABASE_ANON_KEY = eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
GEMINI_API_KEY = tu-clave-aqui
GOOGLE_API_KEY = tu-clave-aqui (opcional)
```

### 2. Conectar Repositorio

1. Ve a [netlify.com](https://netlify.com)
2. Haz login con GitHub
3. Haz clic en "New site from Git"
4. Selecciona tu repositorio de `gasto-facil`
5. Netlify detectará automáticamente `netlify.toml`

### 3. Configuración de Build

- **Build command**: `npm run build`
- **Publish directory**: `public`

Netlify debería auto-detectar esto desde `netlify.toml`.

### 4. Deploy

¡Listo! Netlify deployará automáticamente en cada push a `main`.

## Características

✅ PWA lista para instalar  
✅ Funciona offline (Service Worker)  
✅ OCR automático de tickets  
✅ Sincronización con Supabase  
✅ HTTPS incluido  
✅ Sin servidor (serverless)  

## URLs Importantes

- **Frontend PWA**: Tu dominio de Netlify (ej: `gasto-facil.netlify.app`)
- **API de Análisis**: `/.netlify/functions/analizar-ticket`
- **Base de datos**: Supabase

## Troubleshooting

### Función retorna 404
- Verifica que `netlify.toml` especifica `functions = "netlify/functions"`
- Las funciones en `netlify/functions/*.js` son auto-detectadas

### SPA no funciona (rutas retornan 404)
- Verifica que `netlify.toml` tiene el redirect `from = "/*"` a `index.html`
- Los archivos estáticos se sirven desde `public/`

### Errores de CORS en API de Gemini/Google
- Las Netlify Functions tienen límites de timeout (10 segundos por defecto)
- Para imágenes grandes, considera reducir el tamaño antes de enviar

## Desarrollo Local

Para probar localmente con las mismas funciones:

```bash
npm install -g netlify-cli
npm run dev
```

Esto inicia un servidor local que emula el ambiente de Netlify.
