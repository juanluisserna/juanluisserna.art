# Juan Luis Serna - Fotografía Profesional

## Sobre el proyecto
Página web personal de fotografía profesional para conseguir más clientes y mejorar la experiencia de entrega de archivos.

- **URL:** www.juanluisserna.art
- **Hosting:** GitHub Pages (gratuito)
- **Repositorio:** https://github.com/juanluisserna/juanluisserna.art
- **Dominio:** Namecheap (DNS configurado para GitHub Pages)
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
├── CNAME               # Dominio personalizado para GitHub Pages
├── .gitignore          # Archivos excluidos del repositorio
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
- Opciones: Portfolio Deportivo (PDF), Portfolio Bodas (PDF), Portal de Clientes, Contacto
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

### 8. Animaciones de cámara (UI)

#### Efecto de enfoque (Focus Effect)
- Cuando cambia la foto, inicia con blur y transiciona a enfocada
- Clases CSS: `.focusing` (blur 8px, scale 1.02) → `.focused` (blur 0, scale 1)
- Simula el autoenfoque de una cámara real

#### Tira de película (Film Strip)
- Barra horizontal en la parte inferior con miniaturas de fotos
- Muestra todas las fotos de la categoría actual
- Click en miniatura navega a esa foto
- Se oculta en modo galería, visible en modo foto individual
- Clase CSS: `.film-strip`, se activa con `.visible`

#### Dial de modo (Mode Dial)
- Selector circular que simula el dial de una cámara
- Muestra las 6 categorías alrededor del dial
- Click en categoría la selecciona y rota el dial
- Integrado en el panel derecho de controles

### 9. Portal de Clientes
- Accesible desde: Menú > Portal de Clientes
- **Página dedicada:** `portal.html` con diseño limpio (fondo blanco, colores amigables)
- Sistema de acceso mediante código único por cliente
- Redirección a página de galería después de ingresar código válido
- Galería con grid responsive y efecto hover
- **Lightbox:** Ver fotos en grande con navegación por flechas
- Descarga individual de fotos con botón overlay
- **Descarga masiva via MEGA:** El botón "Descargar todas" abre el enlace de MEGA
- Acceso directo vía URL: `portal.html?code=demo-2024`

**Integración con MEGA (para entregas grandes):**
- Las fotos de previsualización (resolución media) se guardan en GitHub Pages
- Las fotos en alta resolución se suben a MEGA (20GB gratis)
- El botón "Descargar todas" abre automáticamente la carpeta de MEGA
- Si no hay megaLink, descarga las fotos del servidor (comportamiento anterior)

**Cómo añadir nuevos clientes:**
1. Crear carpeta en `/images/clients/` con el código (ej: `perez-boda-2024`)
2. Exportar fotos en dos versiones:
   - **Previsualizaciones** (1200-1600px de ancho) → copiar a `/images/clients/perez-boda-2024/`
   - **Alta resolución** (originales) → subir a carpeta en MEGA
3. Crear carpeta en MEGA y obtener el enlace compartido (Clic derecho > Obtener enlace)
4. Añadir entrada en `clientGalleries` en **AMBOS archivos** (`index.html` y `portal.html`):
```javascript
"perez-boda-2024": {
  name: "Pérez & García Wedding",
  nameEs: "Boda Pérez & García",
  date: "March 10, 2024",
  dateEs: "10 de Marzo, 2024",
  megaLink: "https://mega.nz/folder/XXXXXX#YYYYYY",  // Enlace de MEGA
  photos: ["preview1.jpg", "preview2.jpg", ...]      // Previsualizaciones
}
```
5. Enviar al cliente el código: `perez-boda-2024`
5. O enviar link directo: `tudominio.com/portal.html?code=perez-boda-2024`

**Código de prueba:** `demo-2024`

## Funcionalidades pendientes (por prioridad)

### Alta prioridad (para conseguir más clientes)
1. **Testimonios** - Sección con opiniones de clientes anteriores (prueba social)
2. **og-image.jpg** - Imagen 1200x630px para compartir en redes (WhatsApp, Instagram, Facebook)

### Media prioridad
3. **Cotizador/Paquetes** - Mostrar servicios y precios para filtrar clientes serios
4. **Blog/Historias** - Publicar sesiones completas (mejora SEO + muestra trabajo en contexto)
5. **Galería de bodas destacadas** - Página dedicada solo a bodas (especialidad principal)

### Marketing externo (no técnico)
- Google My Business - Perfil gratuito para búsquedas locales en Barcelona
- Instagram consistente - 3-4 posts/semana con hashtags locales (#fotografobodabarcelona)
- Colaboraciones - Wedding planners, floristas, venues para referidos
- Reseñas en Google - Pedir a clientes satisfechos
- Bodas.net / Zankyou - Directorios de bodas

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
- `updateFilmStrip()` - Actualiza las miniaturas de la tira de película
- `updateModeDial()` - Actualiza la rotación del dial de modo

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
- `.focusing` - Estado de enfocando (blur, scale)
- `.focused` - Estado enfocado (sin blur)
- `.film-strip` - Contenedor de la tira de película
- `.film-strip.visible` - Tira de película visible
- `.film-thumb` - Miniatura en la tira de película
- `.mode-dial` - Dial selector de modo/categoría

## Sistema de entrega actual
- **Portal de Clientes integrado** - Cada cliente recibe un código único para acceder a su galería privada
- **MEGA** para descargas en alta resolución (20GB gratis, sin límite de descarga)
- Las previsualizaciones se ven en el portal, la descarga completa va a MEGA

## Redes sociales
- Instagram: @juanluisserna_foto
- WhatsApp: +34 653 413 157

## Hosting y Deployment

### GitHub Pages (actual)
- **Repositorio:** https://github.com/juanluisserna/juanluisserna.art
- **Branch:** main
- **Dominio personalizado:** juanluisserna.art (configurado en Settings > Pages)

### Para subir cambios al sitio web
```bash
cd ~/Documents/juanluisserna.art
git add .
git commit -m "Descripción del cambio"
git push
```
Los cambios se publican automáticamente en 1-2 minutos.

### Configuración DNS (Namecheap)
El dominio está en Namecheap con los siguientes registros:
- **A Records** (apuntan a GitHub Pages):
  - 185.199.108.153
  - 185.199.109.153
  - 185.199.110.153
  - 185.199.111.153
- **CNAME Record:** www → juanluisserna.github.io

### Archivos excluidos del repositorio (.gitignore)
- Carpetas "Tamaño original" (archivos muy grandes)
- Archivos .ARW (RAW de cámara)
- Archivos .MP4/.mp4 (videos)
- Respaldo*.html (versiones anteriores)
- Archivos temporales y de sistema

## Para probar localmente (antes de subir cambios)
```bash
cd ~/Documents/juanluisserna.art
python3 -m http.server 3000
# Abrir http://127.0.0.1:3000
```
**Notas:**
- No abrir el archivo directamente con `file://` - causa problemas con rutas relativas
- Usar `127.0.0.1:3000` en lugar de `localhost:3000` (más confiable)
- Después de probar, subir cambios con `git add . && git commit -m "mensaje" && git push`

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
- El archivo index.html tiene ~2500 líneas - todo está en un solo archivo (HTML, CSS, JS)
- Los textos de las fotos individuales (photo.title) están mayormente vacíos, solo la primera foto de cada categoría tiene título
- El body/descripción está en la categoría, no en cada foto individual
