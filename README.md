# 🚛 Mi Grúa 24/7 - PWA Profesional

Aplicación web progresiva (PWA) de alto rendimiento para servicio de grúa de plataforma en Costa Rica.

## ✨ Características

- ⚡ **PWA Completa**: Funciona offline, instalable en cualquier dispositivo
- 📱 **100% Responsive**: Optimizada para iOS, Android y Desktop
- 🎨 **Diseño Moderno**: Interfaz profesional con animaciones fluidas
- 🚀 **Ultra Rápida**: Carga instantánea con service workers
- 📞 **WhatsApp Integration**: Formulario conectado directamente a WhatsApp
- 🔍 **SEO Optimizado**: Schema.org markup, Open Graph, meta tags completos
- ♿ **Accesible**: Diseño inclusivo y navegable

## 🛠️ Stack Tecnológico

- **Frontend**: React 18 (via CDN)
- **Estilos**: Tailwind CSS
- **Iconos**: Lucide React
- **PWA**: Service Worker + Manifest
- **Deployment**: Vercel, GitHub Pages, o servidor propio

## 📦 Estructura del Proyecto

```
mi-grua-247/
├── index.html          # Página principal con React
├── manifest.json       # Configuración PWA
├── sw.js              # Service Worker para cache
├── package.json        # Configuración del proyecto
├── vercel.json        # Configuración Vercel
├── README.md          # Este archivo
└── public/            # Assets (crear esta carpeta)
    ├── icon-192.png
    ├── icon-512.png
    ├── icon-96.png
    └── favicon.ico
```

## 🚀 Deployment

### Opción 1: Vercel (Recomendado - Más Rápido)

1. **Instalar Vercel CLI** (opcional):
   ```bash
   npm install -g vercel
   ```

2. **Deployment directo desde GitHub**:
   - Ve a [vercel.com](https://vercel.com)
   - Conecta tu cuenta de GitHub
   - Click en "Import Project"
   - Selecciona tu repositorio
   - ¡Deployment automático! ⚡

3. **O deployment desde terminal**:
   ```bash
   vercel
   # Sigue las instrucciones
   vercel --prod  # Para producción
   ```

4. **Configurar dominio personalizado** (opcional):
   - En el dashboard de Vercel
   - Settings → Domains
   - Agregar tu dominio

### Opción 2: GitHub Pages

1. **Crear repositorio en GitHub**:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/tu-usuario/mi-grua-247.git
   git push -u origin main
   ```

2. **Habilitar GitHub Pages**:
   - Ve a Settings → Pages
   - Source: Branch `main`, folder `/ (root)`
   - Save

3. **Tu sitio estará en**: `https://tu-usuario.github.io/mi-grua-247/`

### Opción 3: Servidor Propio

#### Con Apache:

1. **Subir archivos** al directorio web (ej: `/var/www/html/`)

2. **Configurar .htaccess**:
   ```apache
   <IfModule mod_rewrite.c>
     RewriteEngine On
     RewriteBase /
     RewriteRule ^index\.html$ - [L]
     RewriteCond %{REQUEST_FILENAME} !-f
     RewriteCond %{REQUEST_FILENAME} !-d
     RewriteRule . /index.html [L]
   </IfModule>
   
   # Habilitar compresión
   <IfModule mod_deflate.c>
     AddOutputFilterByType DEFLATE text/html text/css application/javascript
   </IfModule>
   
   # Cache headers
   <IfModule mod_expires.c>
     ExpiresActive On
     ExpiresByType image/png "access plus 1 year"
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType application/javascript "access plus 1 month"
   </IfModule>
   ```

#### Con Nginx:

```nginx
server {
    listen 80;
    server_name migrua247.com www.migrua247.com;
    root /var/www/mi-grua-247;
    index index.html;

    # Compresión
    gzip on;
    gzip_types text/css application/javascript image/svg+xml;

    # Cache
    location ~* \.(png|jpg|jpeg|gif|ico|svg)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    location ~* \.(css|js)$ {
        expires 1M;
        add_header Cache-Control "public";
    }

    # PWA files
    location ~ ^/(manifest\.json|sw\.js)$ {
        add_header Cache-Control "no-cache";
    }

    # Fallback a index.html
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## 🎨 Crear los Iconos/Assets

La PWA necesita iconos. Puedes crearlos de varias formas:

### Opción A: Generador Online
1. Usa [Favicon Generator](https://realfavicongenerator.net/)
2. Sube un logo (preferiblemente 512x512)
3. Descarga el paquete completo
4. Coloca los archivos en `/public/`

### Opción B: Crear Manualmente
Crea imágenes PNG con estas dimensiones:
- `icon-512.png` (512x512) - Icono principal
- `icon-192.png` (192x192) - Icono estándar
- `icon-96.png` (96x96) - Shortcuts
- `favicon.ico` (32x32) - Favicon

**Tip**: Usa el color amarillo-ámbar (#f59e0b) como principal para mantener consistencia con el brand.

## 🔧 Personalización

### Cambiar Número de WhatsApp
Buscar y reemplazar `50687409343` con tu número:
```javascript
// En index.html, línea del WhatsApp URL
const whatsappURL = `https://wa.me/TU_NUMERO?text=${mensaje}`;
```

### Modificar Colores
Los colores principales están en Tailwind. Busca estos valores:
- `amber-500`: Color principal (#f59e0b)
- `slate-900`: Fondo oscuro (#0f172a)

### Cambiar Zonas de Cobertura
En el componente, sección "Coverage":
```javascript
{[
  'San José Centro', 'Escazú', // ... agregar más zonas
].map(...)}
```

## 📊 SEO y Analytics

### Google Search Console
1. Verifica propiedad en [search.google.com/search-console](https://search.google.com/search-console)
2. Envía el sitemap (se genera automático en `/sitemap.xml`)
3. Monitorea indexación y performance

### Google Analytics (Opcional)
Agregar antes de `</head>` en index.html:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

## ⚡ Optimización de Performance

La PWA ya está optimizada con:
- ✅ Service Worker para cache
- ✅ Lazy loading de imágenes
- ✅ Compresión de assets
- ✅ CDN para librerías
- ✅ Minificación CSS/JS

### Test de Performance
```bash
# Lighthouse CI (recomendado)
npm install -g @lhci/cli
lhci autorun --url=https://tu-sitio.com

# O usa PageSpeed Insights:
# https://pagespeed.web.dev/
```

## 🐛 Solución de Problemas

### Service Worker no se registra
- Verifica que estés usando HTTPS (o localhost)
- Revisa la consola del navegador para errores
- Asegúrate que `sw.js` esté en la raíz

### Los iconos no aparecen
- Verifica las rutas en `manifest.json`
- Asegúrate que los archivos PNG existen
- Limpia caché del navegador

### WhatsApp no abre
- Verifica el formato del número: `+506XXXXXXXX`
- No uses espacios ni guiones en el número
- URL debe ser: `https://wa.me/50687409343`

## 📱 Testing

### Desktop
- Chrome, Firefox, Safari, Edge

### Mobile
- iOS Safari
- Android Chrome
- Samsung Internet

### PWA Installation
1. Abre el sitio en Chrome mobile
2. Menú → "Agregar a pantalla de inicio"
3. Verifica que funcione offline

## 📄 Licencia

MIT License - libre para uso comercial

## 📞 Soporte

Para modificaciones o soporte:
- Email: dev@migrua247.com
- WhatsApp: +506 8740-9343

---

**Desarrollado con ❤️ para Mi Grúa 24/7**

¡Tu servicio de grúa ahora tiene presencia digital profesional! 🚛✨
