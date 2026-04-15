# Dimensiones de imágenes — Futool Theme
> Referencia para el equipo de diseño. Dimensiones basadas en el CSS del tema a resolución estándar **1920 × 1080 px**.

---

## 1. Hero Banner

| Asset | Dimensiones | Ratio | Formato |
|---|---|---|---|
| **Imagen principal del banner** | **1920 × 984 px** | ~2:1 | JPG / WEBP |

- Ocupa el 100% del ancho y toda la altura de la ventana menos el header (~96px).
- Usa `object-fit: cover` → lo importante debe estar centrado.
- Es la primera imagen que carga (`loading: eager`) — **prioridad alta**, optimizar para web.

---

## 2. Tarjetas de Categoría (Hero)

| Asset | Dimensiones | Ratio | Cantidad |
|---|---|---|---|
| **Imagen por tarjeta** | **400 × 700 px** | ~4:7 (retrato) | 6 imágenes |

- Se muestran superpuestas al fondo del hero en fila horizontal.
- Usa `object-fit: cover` — enfocar el producto al centro.
- Etiqueta de color (nombre de categoría) se superpone arriba (~36px).

---

## 3. Banner Publicitario

| Asset | Dimensiones | Ratio | Formato |
|---|---|---|---|
| **Imagen del banner** | **1920 × 490 px** | ~4:1 | JPG / WEBP |

- Ocupa el 100% del ancho con altura fija de ~45vh (~486px a 1080p).
- Usa `object-fit: cover`.
- Puede llevar enlace a colección o promoción.

---

## 4. Cuadrícula de Ofertas (5 imágenes)

La grilla tiene un layout asimétrico. Las 5 imágenes tienen posiciones fijas:

| # | Posición | Dimensiones | Ratio |
|---|---|---|---|
| **#1** | Grande izquierda (columna 1, filas 1+2) | **430 × 625 px** | ~2:3 (retrato) |
| **#2** | Ancha arriba derecha (columnas 2-4, fila 1) | **800 × 380 px** | ~2:1 (paisaje) |
| **#3** | Pequeña inferior izquierda (columna 2, fila 2) | **270 × 240 px** | ~9:8 (cuasi cuadrado) |
| **#4** | Pequeña inferior centro (columna 3, fila 2) | **270 × 240 px** | ~9:8 (cuasi cuadrado) |
| **#5** | Pequeña inferior derecha (columna 4, fila 2) | **270 × 240 px** | ~9:8 (cuasi cuadrado) |

- Todas usan `object-fit: cover`.
- Todas tienen `border-radius: 6px`.

---

## 5. Banner Mercado Libre

| Asset | Dimensiones | Ratio | Formato |
|---|---|---|---|
| **Imagen del banner** | **1920 × 380 px** | ~5:1 | JPG / WEBP |

- Fondo amarillo de ML (`#FFE600`) visible si la imagen no cubre todo.
- Altura fija ~35vh (~378px a 1080p).
- Siempre abre en pestaña nueva.

---

## 6. Imágenes de Producto (Tarjetas)

| Asset | Dimensiones | Ratio | Formato |
|---|---|---|---|
| **Foto de producto** | **600 × 600 px** | 1:1 (cuadrado) | JPG / WEBP |

- Usadas en secciones **Recomendados** y **Vitrina**.
- Usa `object-fit: contain` con fondo blanco — no recorta el producto.
- Fondo debe ser **blanco puro (#FFFFFF)** o transparente.

---

## 7. Logo Header

| Asset | Dimensiones | Formato |
|---|---|---|
| **Logo horizontal** | **200 × 60 px aprox.** | PNG con transparencia |

---

## 8. Logo Footer

| Asset | Dimensiones | Formato |
|---|---|---|
| **Logo vertical** | **120 × 160 px aprox.** | PNG con transparencia |

---

## Notas generales

- Todos los archivos deben entregarse en **WEBP** como primer formato y **JPG** como fallback.
- Peso máximo recomendado: banners ≤ 200 KB, productos ≤ 80 KB, ofertas ≤ 120 KB.
- Shopify hace resize automático en el servidor — entregar al **tamaño nativo indicado** (no escalar de más).
- Los tamaños en píxeles son para pantallas **1x**. Para pantallas Retina/2x, entregar el doble de resolución si es posible.
