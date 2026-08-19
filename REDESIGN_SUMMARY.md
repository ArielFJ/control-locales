# Rediseño UI — Control de Locales

## Resumen

Rediseño completo del front-end según el brief (inspiración Stripe + Linear light), ejecutado a mano (no por agente) tras dos intentos fallidos de OpenCode que se colgaron en modo no-interactivo.

## Cambios visuales aplicados

- **Sidebar**: nuevo estilo dark premium (gradiente azul petróleo `#0d1526 → #0f172a → #16213a`), iconos alineados, indicador activo con barra lateral brillante, etiqueta "Menú", navegación más limpia. Reemplaza el gradiente azul plano anterior.
- **Tipografía**: Inter (Google Fonts) con pesos 400-800, números financieros con `font-variant-numeric: tabular-nums`, títulos con letter-spacing negativo.
- **Paleta**: fondo `#f7f8fa`, superficies blancas, bordes `#e5e9f0`, texto `#0f172a` / secundario `#64748b`, acento interactivo violeta `#533afd` en focus rings.
- **KPIs**: de gradientes fuertes a tarjetas blancas con borde sutil, icono en chip de color (bg tintado + color de estado), valor grande bold, label uppercase.
- **Tablas**: cabeceras con fondo sutil `#f8fafc`, hover en filas, badges estilo chip tintado con bordes, alineación numérica tabular.
- **Botones**: primario azul con hover/elevación, secundario blanco, WhatsApp `#25D366`, tamaños táctiles.
- **Gráfico de barras**: barras redondeadas con gradiente azul, tooltips, etiquetas limpias, altura aumentada (180px).
- **Modales**: con backdrop blur, animación fade + scale, sombra profunda.
- **Responsive**: sidebar → drawer con hamburguesa, KPIs 2 col en móvil, inputs 44px táctiles, formularios full-width en móvil.

## Funcionalidad preservada (CRÍTICO)

- **Todo el JavaScript intacto** (285+ líneas): datos localStorage, renderizado de tablas, recibos jsPDF, export CSV, WhatsApp deep links, navegación por pestañas, backup/restore.
- **Todos los 48 IDs** requeridos presentes y verificados.
- **Todas las clases funcionales** (.tab, .badge, .kpi, .btn, .form-grid, .table-wrap, .modal, .recibo, .empty-state, .hidden, .no-print, .hamburguer, .toolbar, .sec, .card, .bars, .bar) mantenidas.
- **Vista de impresión** de recibos conservada.
- **Recibo formal** (monospace, bordes, firmas) intacto — es documento administrativo.

## Bug corregido (de regalo)

El JS usaba `document.getElementById('p-edit')` en `guardarPago()` y `editarPago()` pero el input oculto `p-edit` **no existía en el HTML original**. Se agregó `<input type="hidden" id="p-edit">` en la sección de pagos para que la edición de pagos funcione correctamente (antes `?.` evitaba el crash pero la edición se perdía al guardar).

## Verificación

- ✅ `node --check` — sintaxis JS válida
- ✅ 48 IDs presentes
- ✅ App cargada en navegador: KPIs correctos, tabla mora, gráfico 12 barras, navegación entre 7 secciones OK
- ✅ Recibo se genera (título + firmas + monto en letras)
- ✅ Sin errores JS en consola
- ✅ CSS computado verificado (sidebar 260px dark, Inter, KPIs blancos con borde, inputs 44px)
