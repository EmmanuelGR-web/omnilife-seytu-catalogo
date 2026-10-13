# Catálogo OMNILIFE · SEYTÚ

Catálogo web público con los productos de nutrición **OMNILIFE** y de cosmética **SEYTÚ** disponibles en Argentina. Cada producto tiene foto, precio de lista, descripción, para qué sirve, cómo y cuándo usarlo, ingredientes y características. El cliente lo abre desde un link, mira los productos y consulta por WhatsApp.

🌐 **Sitio publicado:** https://omnilife-seytu.netlify.app

> Sitio realizado por **NeoEmaTech** para un distribuidor independiente de OMNILIFE y SEYTÚ. No es un sitio oficial de la empresa.

---

## ¿Para qué sirve?

- Mostrar el catálogo completo (98 productos) de forma ordenada y fácil de recorrer desde el celular.
- Que el cliente entienda cada producto sin tener que preguntar: qué es, para qué sirve, cómo usarlo, qué lleva.
- Convertir las consultas en ventas con un botón directo a WhatsApp.
- Permitir descargar el catálogo como PDF.
- Presentar a la empresa (sección "Quiénes somos") para generar confianza.

## Funcionalidades

| Función | Detalle |
|---|---|
| Catálogo | 98 productos: 39 de nutrición OMNILIFE y 59 de cosmética SEYTÚ |
| Ficha de producto | Foto, categoría, precio, presentación, ¿para qué sirve?, ingredientes, cómo y cuándo usarlo, características |
| Búsqueda | Búsqueda en vivo por nombre o texto |
| FILTRAR | Panel con todos los filtros: línea, categoría y orden (destacados, menor/mayor precio, A–Z) |
| Quiénes somos | Historia, cifras, marcas, calidad y cómo comprar |
| WhatsApp | Botones de contacto con mensaje prearmado |
| Guardar PDF | Genera el catálogo completo para imprimir o guardar |
| Responsive | Pensado primero para celular (1 columna), luego 2 y 3 columnas en pantallas grandes |
| Tema | Colores de OMNILIFE (violeta y naranja), con modo oscuro automático |

## Tecnologías usadas

- **HTML5, CSS3 y JavaScript** puros, sin frameworks ni librerías. Un solo archivo (`index.html`).
- **CSS**: variables (design tokens), Grid y Flexbox, `prefers-color-scheme` para el modo oscuro, `@media print` para el PDF.
- **Google Fonts**: Montserrat y Noto Sans.
- **Imágenes**: fotos originales desde el CDN de OMNILIFE, con foto de respaldo embebida en base64 (JPEG) por si alguna no carga.
- **WhatsApp**: enlaces `wa.me` con mensaje inicial.
- **PDF**: `window.print()` con estilos de impresión, precargando todas las imágenes antes de abrir el diálogo.
- **Python** (Pillow, NumPy, SciPy): preparación de las fotos de respaldo (recorte, limpieza de etiquetas y formato).
- **Netlify**: hosting estático.
- **Git y GitHub**: control de versiones.

## ¿Cómo funciona?

1. **Datos.** Los productos están en un arreglo de JavaScript (`var P=[...]`). Cada fila tiene: línea (`N` nutrición / `S` Seytú), categoría, nombre, presentación, descripción, uso, precio y marcas (`L` lanzamiento, `M` más vendido).
2. **Información ampliada.** Los textos de "¿Para qué sirve?", "Cómo y cuándo usarlo" y "Características" están en el arreglo `X`. Los ingredientes y características extra se suman desde el arreglo `Y`.
3. **Fotos.** Se cargan desde el CDN de OMNILIFE (`URLS`). Si una foto falla, queda vacía o tarda más de unos 6 segundos, la página la reemplaza sola por la foto de respaldo (`IMG`).
4. **Renderizado.** El JavaScript genera las tarjetas según la búsqueda y los filtros activos.
5. **Vistas.** El menú alterna entre "Productos" y "Quiénes somos" sin recargar la página (`#quienes-somos` abre esa sección directo).
6. **PDF.** Al tocar "Guardar PDF" se limpian los filtros, se despliega toda la información, se cargan todas las fotos y se abre la impresión del navegador.

## Estructura del repositorio

```
├── index.html              # Sitio completo, listo para publicar (incluye las fotos de respaldo)
├── template.html           # Fuente editable (precios, textos, estilos)
├── x.js                    # Textos ampliados por producto (referencia)
├── y.js                    # Ingredientes y características extra (referencia)
├── fotos/                  # Fotos de respaldo (000.jpg = primer producto)
├── logo_clean.png          # Logo de NeoEmaTech
├── catalogo-netlify.zip    # index.html comprimido, para subir a mano a Netlify
├── netlify.toml            # Configuración de Netlify
└── README.md
```

> `template.html` lleva un marcador (`/*IMGS*/[]`) donde se insertan las fotos de respaldo en base64. `index.html` es el resultado ya armado.

## Cómo actualizar los precios

1. Abrí `template.html` y buscá el arreglo `var P=[`.
2. En cada fila, el número es el precio de lista en pesos (por ejemplo `63000`). Es el penúltimo valor de la fila.
3. Generá nuevamente `index.html` insertando las fotos de respaldo en el marcador `/*IMGS*/[]`.
4. Publicá el cambio.

Más fácil: pedirle a Claude "actualizá los precios" con la lista nueva, y volver a publicar.

## Cómo publicarlo

**Con Netlify (subida manual):** en el sitio, pestaña **Deploys**, tocá **browse files to upload** y elegí `catalogo-netlify.zip`.

**Con GitHub (automático):** en Netlify, **Project configuration → Build & deploy → Link repository** y elegí este repositorio. Cada cambio en `main` se publica solo.

## Notas importantes

- Los precios son de **lista al público**, con impuestos, y están sujetos a cambios.
- La información de cada producto se basa en el portal de OMNILIFE Argentina y en fichas públicas de otros países. **La composición puede variar según el país: revisá siempre la etiqueta del envase.**
- Los suplementos dietarios son complementos de la dieta, no medicamentos, y no sirven para diagnosticar, tratar ni curar enfermedades.
- Las certificaciones mencionadas en "Quiénes somos" corresponden a las instalaciones indicadas por la empresa, no son una aprobación individual de cada producto.
- OMNILIFE y SEYTÚ son marcas de sus respectivos titulares. Este catálogo es de un distribuidor independiente.

## Créditos

Desarrollado por **NeoEmaTech**. Todos los derechos reservados.
