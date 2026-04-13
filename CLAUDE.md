# CLAUDE.md — Futool Theme (Shopify)

Guía de referencia rápida para que cualquier IA pueda leer, entender y modificar este tema con precisión.

---

## Datos del proyecto

| Campo | Valor |
|---|---|
| Nombre del tema | Futool Theme |
| Versión | 1.0.0 |
| Autor | Futool Internacional |
| Sitio | futoolmexico.com |
| Idioma principal | Español (`es`) |
| Plataforma | Shopify (Liquid) |

---

## Estructura de archivos

```
/
├── assets/
│   └── theme.css              # Única hoja de estilos global
├── config/
│   ├── settings_data.json     # Valores actuales de configuración del tema
│   └── settings_schema.json   # Esquema de ajustes del tema (solo theme_info)
├── layout/
│   └── theme.liquid           # Layout principal: <html>, <head>, header, footer
├── locales/
│   └── es.default.json        # Traducciones en español
├── sections/                  # Secciones de Shopify (cada una incluye {% schema %})
│   ├── header.liquid
│   ├── footer.liquid
│   ├── hero.liquid
│   ├── recommended-products.liquid
│   ├── advertising-banner.liquid
│   ├── offers-grid.liquid
│   ├── mercadolibre-banner.liquid
│   ├── showcase.liquid
│   └── benefits.liquid
├── snippets/
│   ├── product-card.liquid    # Tarjeta de producto reutilizable
│   └── svg-icons.liquid       # Sprite SVG inline (renderizado en layout)
└── templates/
    ├── index.json             # Página de inicio (orden y configuración de secciones)
    └── search.bss.b2b.liquid  # Plantilla de búsqueda B2B
```

---

## Layout principal (`layout/theme.liquid`)

- Carga `theme.css` con `{{ 'theme.css' | asset_url | stylesheet_tag }}`.
- Renderiza el sprite SVG: `{%- render 'svg-icons' -%}` (debe ir antes del header).
- Estructura: `<body class="app">` → `svg-icons` → `section 'header'` → `<main class="page">{{ content_for_layout }}</main>` → `section 'footer'`.

---

## Página de inicio (`templates/index.json`)

Orden de secciones en la homepage:

1. `hero` → tipo `hero`
2. `recommended` → tipo `recommended-products`
3. `advertising` → tipo `advertising-banner`
4. `offers` → tipo `offers-grid`
5. `mercadolibre` → tipo `mercadolibre-banner`
6. `showcase` → tipo `showcase`
7. `benefits` → tipo `benefits`

Para agregar o reordenar secciones, editar este archivo JSON.

---

## Convención de clases CSS

El tema usa un patrón BEM-like con sufijos dobles (`__`):

```
[elemento]__[bloque]        → ej. content__footer, actions__navigation
[elemento]__[bloque]-[mod]  → ej. img__card-app, btn__card-app
```

Clases raíz de cada sección/componente principal:

| Clase raíz | Sección/componente |
|---|---|
| `.navigation` | Header |
| `.footer` | Footer |
| `.hero` | Hero banner |
| `.recommended` | Productos recomendados |
| `.advertising` | Banner publicitario |
| `.offers` | Cuadrícula de ofertas |
| `.mercadolibre` | Banner Mercado Libre |
| `.showcase` | Vitrina de productos |
| `.benefits` | Beneficios |
| `.product__card-app` | Tarjeta de producto |

---

## Secciones — Referencia rápida

### `header.liquid`
**Clase raíz:** `.navigation`

**Settings del schema:**
| ID | Tipo | Descripción |
|---|---|---|
| `logo` | `image_picker` | Logo horizontal (fallback: `logoHorizontal.png`) |
| `billing_url` | `url` | URL para enlace de facturación |

**Funcionalidad JS interna:**
- Botón hamburguesa `.hamburger__nav` abre/cierra `#mobile-nav` con clase `is-open`.
- Nav desktop: dropdowns con clase `.has-dropdown` y `.dropdown__nav`.
- Colecciones filtradas por título: `contains 'maquinaria'` y `contains 'refaccion'`.

---

### `footer.liquid`
**Clase raíz:** `.footer`

**Settings del schema (todos opcionales):**
| ID | Tipo | Descripción |
|---|---|---|
| `logo_vertical` | `image_picker` | Logo vertical (fallback: `logoVertical.png`) |
| `phone_1`, `phone_2` | `text` | Teléfonos |
| `whatsapp_1/2/3` | `text` | Números WhatsApp (texto visible) |
| `info_menu` | `link_list` | Menú de información |
| `payment_menu` | `link_list` | Menú de formas de pago |
| `billing_menu` | `link_list` | Menú de facturación |
| `attention_hours` | `text` | Horario de atención L-V |
| `attention_saturday` | `text` | Horario sábado |
| `email` | `text` | Email de contacto |
| `catalog_url` | `url` | URL para descarga de catálogos |
| `whatsapp_link` | `url` | Link redes sociales WhatsApp |
| `facebook_link` | `url` | Link Facebook |
| `instagram_link` | `url` | Link Instagram |
| `tiktok_link` | `url` | Link TikTok |
| `show_visa/mastercard/amex/oxxo` | `checkbox` | Mostrar ícono de pago |

---

### `hero.liquid`
**Clase raíz:** `.hero`

**Settings:** `hero_image` (image_picker) — imagen principal del banner.

**Blocks:** tipo `category_card` (máx. 6)
| ID | Tipo | Default |
|---|---|---|
| `title` | `text` | `"CATEGORÍA"` |
| `image` | `image_picker` | — |
| `link` | `url` | — |

---

### `recommended-products.liquid`
**Clase raíz:** `.recommended`

**Settings:**
| ID | Tipo | Default |
|---|---|---|
| `title` | `text` | `"Recomendados"` |
| `collection` | `collection` | — |

Renderiza **dos filas** de 5 productos usando `{% render 'product-card' %}`. Si hay menos de 5 productos reales, muestra los disponibles; si no hay colección, muestra placeholders.

---

### `advertising-banner.liquid`
**Clase raíz:** `.advertising`

**Settings:** `image` (image_picker), `link` (url, opcional).

---

### `offers-grid.liquid`
**Clase raíz:** `.offers`

**Blocks:** tipo `offer_image` (máx. 5)
| ID | Tipo |
|---|---|
| `image` | `image_picker` |
| `link` | `url` |

---

### `mercadolibre-banner.liquid`
**Clase raíz:** `.mercadolibre`

**Settings:** `image` (image_picker), `url` (url de la tienda ML). Siempre abre en `target="_blank"`.

---

### `showcase.liquid`
**Clase raíz:** `.showcase`

**Settings:**
| ID | Tipo | Rango | Default |
|---|---|---|---|
| `collection` | `collection` | — | — |
| `products_limit` | `range` | 1–10 | `5` |

Usa una sola fila `.products__carrusel-app` con `{% render 'product-card' %}`.

---

### `benefits.liquid`
**Clase raíz:** `.benefits`

**Blocks:** tipo `benefit_item` (sin límite)
| ID | Tipo | Opciones |
|---|---|---|
| `text` | `text` | Libre |
| `icon` | `select` | `icon-shield-check`, `icon-truck`, `icon-building`, `icon-handshake` |

---

## Snippet: `product-card.liquid`

**Uso:**
```liquid
{% render 'product-card', product: product %}
{% render 'product-card', product: nil, placeholder_index: 1 %}  {# placeholder 1–6 #}
```

**Lógica:**
- Calcula descuento si `product.compare_at_price > product.price`.
- Muestra badge `-XX%` cuando hay descuento.
- Botón "Agregar al carrito" hace `POST` a `{{ routes.cart_add_url }}` con `id` = variante disponible.
- Con `product: nil` muestra un placeholder visual con badge `-25%` y botón deshabilitado.

**Clases internas clave:**
- `.product__card-app` — contenedor
- `.discount__card-app` — badge de descuento
- `.img__container__card-app` — figura
- `.img__card-app` — imagen del producto
- `.card-app-title` — título
- `.card-app-description` — descripción (truncada a 70 chars, sin HTML)
- `.price__card-app` — precio actual
- `.original-price__card-app` — precio tachado
- `.btn__card-app` — botón de carrito

---

## Snippet: `svg-icons.liquid`

Sprite SVG inline. Todos los íconos se referencian con `<use href="#ID">`.

**IDs disponibles:**

| ID | Descripción |
|---|---|
| `icon-heart` | Corazón / Favoritos |
| `icon-cart3` | Carrito de compras |
| `icon-person` | Persona / Cuenta |
| `icon-search` | Lupa / Buscar |
| `icon-shield-check` | Escudo con check |
| `icon-truck` | Camión / Envío |
| `icon-building` | Edificio / Ubicación |
| `icon-handshake` | Apretón de manos |
| `icon-whatsapp` | WhatsApp |
| `icon-facebook` | Facebook |
| `icon-instagram` | Instagram |
| `icon-tiktok` | TikTok |
| `icon-pay-visa` | Pago VISA |
| `icon-pay-mastercard` | Pago MasterCard |
| `icon-pay-amex` | Pago American Express |
| `icon-pay-oxxo` | Pago OXXO |

**Para agregar un ícono nuevo:** agregar un `<symbol id="icon-NOMBRE" viewBox="...">` dentro del `<svg>` en `svg-icons.liquid`.

---

## Estilos (`assets/theme.css`)

Archivo CSS único. No hay preprocesadores (Sass/Less). Editar directamente este archivo para cambios de estilos globales.

---

## Locales (`locales/es.default.json`)

Estructura actual:
```json
{
  "general": { "search": { "placeholder": "Buscar producto..." } },
  "cart": { "general": { "title": "...", "empty": "...", "add": "..." } },
  "products": { "product": { "add_to_cart": "...", "sold_out": "..." } }
}
```
Para añadir traducciones, extender este JSON con la clave correspondiente.

---

## Reglas para modificaciones

1. **Para cambiar texto/imágenes configurables** → editar `config/settings_data.json` o los settings de sección en `templates/index.json`.
2. **Para agregar una nueva sección** → crear `sections/nombre.liquid` con su `{% schema %}` al final, luego agregarla al `templates/index.json`.
3. **Para agregar estilos** → solo editar `assets/theme.css`.
4. **Para agregar un ícono SVG** → agregar `<symbol>` en `snippets/svg-icons.liquid` y referenciarlo con `<use href="#icon-nuevo">`.
5. **Para agregar un ítem de navegación** → editar el `<nav>` en `sections/header.liquid` (tanto desktop como el bloque `mobile-nav`).
6. **Para cambiar el orden de secciones en homepage** → modificar el array `"order"` en `templates/index.json`.
7. **El snippet `product-card` no tiene schema**; sus parámetros son `product` y `placeholder_index`.
