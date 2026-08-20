# Rediseño UI — Control de Locales

## Contexto del proyecto
App web PWA de un solo archivo (`index.html` + `manifest.json`) para administrar locales comerciales de alquiler en Santo Domingo, RD. La usa un dueño de propiedades (Padre) desde su teléfono móvil principalmente (Chrome Android, instalada como PWA en pantalla de inicio). También la abre en desktop ocasionalmente.

## CRÍTICO — RESTRICCIONES
1. **NO romper ninguna funcionalidad JS**. El archivo actual tiene ~285 líneas de JS (localStorage, renderizado de tablas, recibos PDF con jsPDF, export CSV, WhatsApp deep links). Mantén TODOS los IDs, clases funcionales, nombres de funciones y estructura de datos intactos. Solo cambia CSS, layout visual y estructura HTML *cuando no afecte el JS*.
2. **Mantener todos los IDs**: dash-sub, mes-selector, kpis, mes-titulo, tbl-mora, chart-cobros, l-local, l-inq, l-tel, l-renta, l-dia, l-estado, l-edit, tbl-locales, p-local, p-fecha, p-monto, p-metodo, tbl-pagos, total-pagos, r-local, r-mes, r-monto, r-numero, r-fecha, recibo-preview, tbl-recibos, wa-morosos, wa-recordatorios, tbl-reporte, c-nombre, c-rnc, c-tel, c-dir, c-email, file-import, modal-bg, modal-box, sidebar, main-nav, brand-sub, tab-dash, tab-locales, tab-pagos, tab-recibos, tab-whatsapp, tab-reporte, tab-backup.
3. **Mantener clases funcionales**: .tab, .active, .badge (.verde/.rojo/.ambar/.gris/.azul), .kpi (.azul/.verde/.rojo/.ambar/.gris/.empty), .btn (.sec/.gris/.verde/.rojo/.wa/.sm/.block), .form-grid, .table-wrap, .modal-bg.show, .recibo y todas sus subclases rec-*, .empty-state, .hidden, .no-print, .hamburguer, .toolbar, .sec, .card, .bars, .bar.
4. **Mantener la vista de impresión** (@media print) para recibos.
5. El recibo debe seguir teniendo aspecto de recibo formal (monospace, bordes, firmas) — es un documento legal/administrativo.

## Dirección de diseño (inspiración Stripe + Linear light)
Busca inspiración en Stripe y Linear (versiones light/clean):
- **Paleta**: Fondo claro `#f7f8fa` / blanco, superficies blancas con bordes sutiles `#e5e9f0`. Azul corporativo como acento (mantener identidad: azul profundo `#1e3a5f` → primario `#245778`), acento interactivo violeta-azul tipo Stripe `#533afd` — usarlo SOLO en CTAs y foco. Texto principal `#0f172a`, secundario `#64748b`. Éxito verde `#16a34a`, alerta ámbar `#d97706`, peligro rojo `#dc2626`.
- **Tipografía**: Inter (Google Fonts) con pesos 400/500/600/700. Números financieros con `font-variant-numeric: tabular-nums`. Títulos con letter-spacing negativo sutil. Cabeceras de sección 20px semibold, tablas 13px.
- **Sombras**: sutiles y azuladas: `0 1px 2px rgba(16,24,40,.04), 0 8px 24px rgba(16,24,40,.06)` para tarjetas. Elevación progresiva en modales.
- **Radio de borde**: 8-12px en tarjetas, 8px en inputs, pills (999px) en badges.
- **Sidebar**: ya no un gradiente azul plano — superficie oscura premium (azul petróleo profundo `#0f172a` o azul degradado elegante) con navegación limpia, iconos alineados, indicador activo con barra lateral sutil. O alternativa: sidebar blanco minimalista con borde derecho. Elige la que se vea más premium — recomiendo dark sidebar para contraste profesional.
- **KPIs**: tarjetas blancas con icono en chip de color suave (bg tintado + icono de color), valor grande bold, label uppercase pequeño. NO gradientes fuertes.
- **Tablas**: cabecera con fondo sutil, filas con hover, badges de estado con chips tintados, alineación numérica derecha, sticky header en desktop.
- **Botones**: primario azul profundo con hover, secundario blanco con borde, WhatsApp verde `#25D366`, botones pequeños para acciones de fila.
- **Chart de barras**: barras redondeadas con gradiente sutil azul, etiquetas limpias, tooltip simple.
- **Responsive mobile-first**: en móvil el sidebar se convierte en drawer (mantener hamburguesa), KPIs en grid 2 cols, tablas scroll horizontal, inputs full-width grandes (min 44px altura táctil), botones táctiles grandes.
- **Micro-interacciones**: transiciones suaves 150-200ms, hover elevación leve, focus rings con `box-shadow 0 0 0 3px rgba(36,87,120,.15)`.
- **Estilo general**: limpio, profesional, de app financiera moderna — que se sienta como una herramienta seria de gestión de propiedades, no como un formulario de los 2000. MUCHA atención al espaciado (jerarquía clara), alineación y densidad de datos.

## Archivos de referencia de diseño
Puedes leer estos archivos para inspiración de tokens:
- `templates/stripe.md` — sistema de diseño Stripe (fintech limpio, sombras azuladas, números tabulares)
- `templates/linear.app.md` — sistema Linear (dark premium, minimalismo preciso)

## Entregable
Reescribe `index.html` manteniendo TODO el JS funcional (líneas 240-525 actuales) y estructura de secciones, aplicando el nuevo diseño CSS. El resultado debe verse notablemente más moderno, premium y profesional que el original.