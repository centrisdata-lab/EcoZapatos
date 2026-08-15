# Flower Miel — Catálogo Digital

Landing page de e-commerce para un apiario/catálogo de productos naturales (miel, propóleo, cosmética, insumos apícolas). Sitio estático, sin build step: HTML + CSS + JS vanilla.

## Estructura

```
index.html              # Página principal (catálogo)
assets/
  css/styles.css        # Todo el CSS del sitio (un solo archivo, ~2000 líneas)
  js/main.js             # Render del grid de productos, filtros, buscador, modal de zoom
  js/cart.js              # Carrito de compras (localStorage) + modal de carrito
  js/purchase.js          # Modal de "comprar" (WhatsApp / Nequi / Bre-B)
  img/                     # Fotos de producto (jpg) + logos (png)
vendedores/index.html   # Variante del catálogo para vendedores (mismo sistema de diseño)
pendon/                 # Piezas gráficas sueltas (pendón de apiturismo), no forman parte del sitio
admin-flowermiel/       # App Node separada con su propia base de datos (Turso) — panel de administración de productos
```

El catálogo (`index.html` + `assets/`) es 100% estático y se despliega en Render con auto-deploy. `admin-flowermiel/` es un proyecto Node aparte que alimenta los datos de producto.

## Sistema de diseño

Ver `.claude/skills/design-system-extraction/` para la skill portable (jerarquía, layout y estilo, sin colores) que documenta el patrón visual de este sitio para poder reaplicarlo a otras marcas.

Resumen rápido de las decisiones de *esta* marca en concreto:

- **Tipografía:** Poppins (headings, weight 700-800) + Quicksand (body, weight 400-600)
- **Paleta:** ámbar/miel como primario (`#e8960c`), verde bosque como secundario (`#3f7d3a`), fondo crema cálido (`#fffaf1`), WhatsApp green (`#25d366`) como color de acción de conversión
- **Forma:** todo redondeado — pills (`border-radius: 999px`) en botones/chips/badges, `radius-lg: 24px` en cards y modales
- **Motivo recurrente:** emoji temático (🐝🍯🌿) como iconografía barata en vez de un set de íconos SVG custom

## Convenciones de prueba

Flujo: implementar → probar en local → push → verificar en producción.

Un solo login de Playwright por sesión de pruebas — el panel admin tiene un rate limiter de 5 intentos / 15 min.

## Notas operativas

- `git push` puede colgarse pidiendo login interactivo de Credential Manager en Windows — si pasa, reintentar o pedirle al usuario que haga el push manualmente.
- Turso (base de datos del admin) es compartida entre local y producción — cuidado al probar operaciones destructivas contra el admin en local.
