# Juan Luis Serna - Fotografía Profesional

## Sobre el proyecto
Página web personal de fotografía profesional para conseguir más clientes y mejorar la experiencia de entrega de archivos.

- **URL actual:** www.juanluisserna.art (usa plantilla de Hostinger, será reemplazada)
- **Proyecto en desarrollo:** index.html local (diseño de cámara, mucho mejor potencial)
- **Hosting actual:** Hostinger (objetivo: migrar a opción gratuita)
- **Ubicación:** España (Barcelona)
- **Especialidad principal:** Bodas y eventos

## Stack técnico actual
- HTML estático (single page)
- CSS inline en el mismo archivo
- JavaScript vanilla
- Sin framework ni bundler
- Diseño: simula la interfaz de una cámara real (pantalla izquierda, controles derecha)

## Estructura del proyecto
```
/home/juanluisserna/Documents/juanluisserna.art/
├── index.html          # Página principal (todo el código aquí)
├── portal.html         # Portal de clientes (página dedicada, fondo blanco)
├── CLAUDE.md           # Este archivo de contexto
├── images/
│   ├── about/          # Fotos personales (aboutme1-4.jpg)
│   ├── portraits/      # Retratos (port1-30.jpg)
│   ├── product/        # Producto (product1-21.jpg)
│   ├── sports/         # Deportes (sp1-32.jpg)
│   ├── travels/        # Viajes (travels1-37.jpg)
│   ├── weddings/       # Bodas (wed1-30.jpg)
│   ├── clients/        # Galerías privadas de clientes
│   │   └── demo-2024/  # Carpeta demo de ejemplo
│   ├── histograms/     # Histogramas para UI de cámara
│   ├── textures/       # Texturas de fondo
│   ├── icons/          # Iconos UI
│   └── logo/           # Logos
├── audio/              # Efectos de sonido (shutter.mp3)
├── portfolios/         # PDFs de portfolio (Deportivo, Bodas, Producto)
└── Respaldo*.html      # Versiones anteriores
```

## Funcionalidades implementadas

### 1. Formulario de contacto
- Servicio: **Web3Forms** (gratuito, sin límites)
- Access Key: `795e4f95-0750-431e-8604-2becad9d7f22`
- Accesible desde: Menú > Contacto
- Campos: nombre, email, teléfono, tipo de evento, fecha, presupuesto (desde 100€), mensaje
- Modal con animación, cierra con X, clic fuera, o tecla Escape

### 2. Sistema de idiomas (ES/EN)
- Selector en esquina superior derecha del header
- Guarda preferencia en localStorage
- Traduce: categorías, descripciones, galería, formulario de contacto, menú
- Objeto `translations` en JavaScript con estructura:
  ```javascript
  translations.es.categories["About Me"].name // "Sobre Mí"
  translations.es.categories["About Me"].body // descripción en español
  ```

### 3. Menú desplegable
- Botón "Menu" en header
- Opciones: Portfolio Deportivo (PDF), Portfolio Bodas (PDF), Contacto
- Posición fija, z-index alto para evitar problemas de superposición

### 4. Sistema de navegación de fotos
- **Nivel 1:** Galería de categorías (6 categorías)
- **Nivel 2:** Galería de fotos dentro de una categoría (botón Gallery desde foto individual)
- **Nivel 3:** Vista de foto individual
- Flujo: Categorías → Seleccionar categoría → Ver foto → Gallery → Ver todas las fotos → Seleccionar foto
- Variables clave: `isGalleryView`, `isPhotoGalleryView`, `selectedPhotoGalleryIndex`
- Layout Masonry (tipo Pinterest) en galería de fotos con scroll vertical

### 5. SEO implementado
- Meta description y keywords optimizados para Barcelona/fotografía
- Open Graph tags para compartir en redes sociales
- Twitter Card meta tags
- Schema.org structured data (LocalBusiness) para Google
- Canonical URL configurada

### 6. Integración de redes sociales
- Enlaces a Instagram (@juanluisserna_foto) y WhatsApp en el footer
- Iconos SVG para mejor rendimiento
- Links con rel="noopener" por seguridad

### 7. Protección de imágenes
- Clic derecho deshabilitado en imágenes
- Arrastrar imágenes deshabilitado
- Atajos de teclado bloqueados (Ctrl+S, Ctrl+U)

### 8. Portal de Clientes
- Accesible desde: Menú > Portal de Clientes
- **Página dedicada:** `portal.html` con diseño limpio (fondo blanco, colores amigables)
- Sistema de acceso mediante código único por cliente
- Redirección a página de galería después de ingresar código válido
- Galería con grid responsive y efecto hover
- **Lightbox:** Ver fotos en grande con navegación por flechas
- Descarga individual de fotos con botón overlay
- Descarga masiva de todas las fotos
- Acceso directo vía URL: `portal.html?code=demo-2024`

**Cómo añadir nuevos clientes:**
1. Crear carpeta en `/images/clients/` con el código (ej: `perez-boda-2024`)
2. Copiar las fotos del cliente a esa carpeta
3. Añadir entrada en `clientGalleries` en **AMBOS archivos** (`index.html` y `portal.html`):
```javascript
"perez-boda-2024": {
  name: "Pérez & García Wedding",
  nameEs: "Boda Pérez & García",
  date: "March 10, 2024",
  dateEs: "10 de Marzo, 2024",
  photos: ["IMG_001.jpg", "IMG_002.jpg", ...]
}
```
4. Enviar al cliente el código: `perez-boda-2024`
5. O enviar link directo: `tudominio.com/portal.html?code=perez-boda-2024`

**Código de prueba:** `demo-2024`

## Funcionalidades pendientes (por prioridad)
1. **Cotizador/Paquetes** - Mostrar servicios y precios
2. **Blog/Historias** - Publicar sesiones y contenido
3. **Testimonios** - Opiniones de clientes anteriores
4. **Imagen og-image.jpg** - Crear imagen para compartir en redes (1200x630px)

## Detalles técnicos importantes

### Rutas de archivos
- Imágenes: `./images/[categoria]/archivo.jpg`
- Audio: `./audio/shutter.mp3`
- Portfolios: `./portfolios/[nombre].pdf`
- **NO usar** `./assets/` - las carpetas están en la raíz

### Estructura JavaScript clave
- `categories[]` - Array con todas las categorías y sus fotos
- `translations{}` - Objeto con traducciones ES/EN
- `currentLang` - Idioma actual ('en' o 'es')
- `updateContent(categoryIndex, photoIndex)` - Actualiza la vista de foto
- `populateGalleryGrid()` - Genera la cuadrícula de categorías
- `populatePhotoGalleryGrid()` - Genera la cuadrícula de fotos dentro de una categoría
- `toggleGalleryView(showGallery)` - Alterna entre galería de categorías y vista de foto
- `togglePhotoGalleryView(showPhotoGallery)` - Alterna entre galería de fotos y vista individual
- `navigatePhotoGallery(direction)` - Navega dentro de la galería de fotos
- `applyTranslations(lang)` - Aplica traducciones al cambiar idioma
- `clientGalleries{}` - Objeto con datos de clientes (código, nombre, fotos)
- `showClientGallery(code)` - Muestra la galería del cliente
- `populatePortalGrid(code, photos)` - Genera el grid de fotos del portal
- `downloadPhoto(code, filename)` - Descarga una foto individual
- `resetPortal()` - Reinicia el portal al estado de login
- `applyPortalTranslations()` - Aplica traducciones del portal

### Clases CSS importantes
- `.hidden` - Oculta elementos (display: none)
- `.active` - Estado activo (modal visible, idioma seleccionado)
- `.menu-item` - Items del menú desplegable
- `.contact-modal` - Modal del formulario de contacto
- `.portal-modal` - Modal del portal de clientes
- `.portal-container` - Contenedor principal del portal
- `.portal-grid` - Grid masonry de fotos del cliente
- `.portal-photo` - Cada foto en el portal
- `.lang-selector` - Selector de idioma
- `.photo-gallery-mode` - Grid de galería de fotos (más columnas, scroll)

## Sistema de entrega actual
- **Portal de Clientes integrado** - Cada cliente recibe un código único para acceder a su galería privada
- Alternativa: Google Drive / Dropbox para entregas muy grandes

## Redes sociales
- Instagram: @juanluisserna_foto
- WhatsApp: +34 653 413 157

## Opciones de hosting gratuito a considerar
- **GitHub Pages** - Gratis, requiere aprender git básico
- **Cloudflare Pages** - Gratis, buen rendimiento
- **Netlify** - Gratis tier, fácil deploy

## Para probar localmente
```bash
cd ~/Documents/juanluisserna.art
python3 -m http.server 3000
# Abrir http://localhost:3000
```
**Notas:**
- No abrir el archivo directamente con `file://` - causa problemas con rutas relativas.
- Si `localhost:3000` no funciona, probar con `127.0.0.1:3000`
- Si sigue sin funcionar, verificar que el servidor esté corriendo (debe mostrar "Serving HTTP on 0.0.0.0 port 3000")
- **Problema conocido:** En algunos sistemas el localhost no resuelve correctamente. Usar la IP directa: `http://127.0.0.1:3000`

## Nivel técnico del usuario
Básico - puede copiar/pegar código y hacer cambios simples. Prefiere recibir código completo para reemplazar.

## Preferencias de trabajo
- Dar código completo cuando se hagan cambios
- Explicar cambios de forma simple
- Evitar terminología técnica compleja
- Hacer respaldos antes de cambios grandes
- Comunicación en español

## Paleta de colores
- Fondo: #4A4A4A (gris oscuro)
- Texto: #E6E6E6 (gris claro)
- Acento: #F28C38 (naranja)
- Fondo oscuro: #1A1A1A, #2A2A2A
- Fuentes: Roboto (texto), Press Start 2P (números retro)

## Notas importantes
- El diseño simula una cámara real - mantener esta estética
- Responsive design es importante (clientes ven desde móvil)
- El archivo index.html tiene ~2000 líneas - todo está en un solo archivo
- Los textos de las fotos individuales (photo.title) están mayormente vacíos, solo la primera foto de cada categoría tiene título
- El body/descripción está en la categoría, no en cada foto individual
