# 🗺️ Croquis — Editor de campus e interiores

[![Demo en vivo](https://img.shields.io/badge/Demo_en_vivo-GitHub_Pages-2ea44f?style=for-the-badge&logo=github)](https://wguandique-2005.github.io/CROQUIS/)

> Demo: [wguandique-2005.github.io/CROQUIS](https://wguandique-2005.github.io/CROQUIS/)

**Croquis** es una aplicación web autónoma para diseñar planos vectoriales de campus y detallar los ambientes interiores de edificios o auditorios. Todo el proyecto reside en un único `index.html`: no requiere instalación, dependencias de Node.js ni compilación.

Está construido con HTML, CSS, JavaScript nativo y SVG. Guarda los cambios localmente y permite exportar el proyecto, imágenes y documentación técnica.

---

## Características

### Plano del campus

- Delimitación editable del terreno, con cálculo de área y perímetro.
- Zonas por polígonos de vértices o dibujo a mano alzada, simplificado con Douglas–Peucker.
- Sellos para edificios, auditorios, canchas, estacionamientos, plazas, baños, piscinas y bodegas.
- Mover, escalar, rotar, duplicar, ordenar por capas, ocultar y bloquear zonas.
- Edición de vértices: inserción en puntos medios y eliminación con `Alt` + clic.
- Vegetación procedural con pincel y goma de radio ajustable.
- Búsqueda y filtros de zonas; la búsqueda también encuentra ambientes interiores.
- Zoom, desplazamiento, encuadre de todo el contenido, rejilla e imán de 10 px.

### Interiores y niveles

Los edificios y auditorios pueden abrirse en una vista de detalle mediante doble clic o con **Editar interiores**.

- Ambientes por nivel: añadir, renombrar o eliminar hasta 20 niveles. Al eliminar un nivel, sus ambientes pasan a planta baja.
- Catálogo editable de ambientes: aulas, laboratorios, oficinas, baños, bodegas, pasillos, escaleras y otros.
- Estampado de ambientes, edición de sus polígonos, movimiento, escala, color, código, descripción y categoría.
- Creación automática de grids por filas y columnas, recortados a la forma real del edificio o del ambiente seleccionado.
- Corte de todos los ambientes atravesados por una línea; `Shift` ajusta el corte a 45°.
- Dibujo manual de ambientes poligonales y representación especial para escaleras.
- Vista 3D isométrica explotada, con control de ángulo y separación entre niveles.

### Exportación y datos

- **PNG:** plano completo a 3200 px en su lado mayor, con cartela y leyenda.
- **PDF con vista previa:** plano de campus, registro jerárquico de zonas y ambientes, planos interiores por nivel y vistas 3D opcionales.
- **JSON:** importación y exportación del estado completo del proyecto.
- **Autoguardado** en `localStorage` y hasta 40 estados de deshacer con `Ctrl` + `Z`.
- **Modo presentación** para visualizar el plano sin paneles.

Las exportaciones se reconstruyen desde los datos SVG, por lo que no dependen del zoom ni de la zona visible en pantalla.

---

## Atajos

| Tecla | Acción |
| :---: | :--- |
| `V` | Seleccionar, mover, escalar, rotar y editar |
| `P` / `F` | Dibujar zona por vértices / a mano alzada |
| `T` | Redibujar el límite del campus |
| `N` / `X` | Pincel / goma de vegetación |
| `B` `A` `C` `E` `G` `H` `S` `D` | Edificio, auditorio, cancha, estacionamiento, plaza, baño, piscina y bodega |
| `R` | Girar 90° la zona seleccionada |
| `Enter` | Cerrar el polígono en curso |
| `Backspace` / `Supr` | Quitar vértice al dibujar o eliminar la selección |
| `Ctrl` + `Z` | Deshacer |
| `Esc` | Cancelar, deseleccionar, cerrar un panel o salir de presentación |

En la vista de interiores: `G` abre el grid, `C` activa el corte y `D` inicia el dibujo de un ambiente.

---

## Estructura del proyecto

```text
CROQUIS/
├── index.html               # Aplicación completa: interfaz, estilos y lógica
├── croquis-campus.json      # Ejemplo de datos exportados
├── croquis-campus-UGB.pdf   # Ejemplo de PDF generado
└── README.md                # Documentación
```

---

## Uso

Abre `index.html` directamente en un navegador moderno o utiliza la [demo en GitHub Pages](https://wguandique-2005.github.io/CROQUIS/). No hay proceso de instalación.

Si prefieres servirlo por HTTP local:

```bash
python3 -m http.server 8000
```

Luego visita `http://localhost:8000/`.

---

## Formato JSON

La exportación conserva el campus, las zonas, la vegetación, la configuración del documento y, dentro de cada edificio o auditorio, sus niveles y ambientes.

```json
{
  "version": 4,
  "terrain": {
    "name": "Campus",
    "points": [{ "x": 200, "y": 160 }]
  },
  "items": [{
    "id": "hl",
    "kind": "bldg",
    "code": "HL",
    "name": "Edificio Hugo Lindo",
    "color": "#D97B2F",
    "visible": true,
    "locked": false,
    "rot": 0,
    "opacity": 0.24,
    "poly": [{ "x": 250, "y": 185 }],
    "nLevels": 2,
    "levelNames": ["PB", "Nivel 1"],
    "rooms": [{
      "id": "r_001",
      "level": 0,
      "cat": "aula",
      "code": "HL-01",
      "name": "Aula",
      "color": "#D9A32E",
      "desc": "",
      "poly": [{ "x": 280, "y": 210 }]
    }]
  }],
  "trees": [{ "x": 420, "y": 310, "r": 9, "tone": 0.65 }],
  "doc": {
    "title": "Croquis del campus",
    "subtitle": "Plano de referencia",
    "author": "Universidad",
    "labelMode": "full",
    "snap": false,
    "grid": false,
    "brushR": 9,
    "eraserR": 36,
    "include3D": true,
    "catalog": []
  }
}
```

`poly` y `terrain.points` deben contener al menos tres puntos para formar una figura válida. Las categorías del catálogo se identifican por `cat` dentro de cada ambiente.

---

## Tecnologías

- HTML5, CSS3 y JavaScript nativo.
- SVG para el renderizado y la edición vectorial.
- Canvas para la exportación de imágenes.
- [jsPDF 2.5.1](https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js) para documentos PDF.
- Google Fonts: [Archivo](https://fonts.google.com/specimen/Archivo) e [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono).

## Licencia

Uso libre para planificación, edición y presentación de planos educativos e institucionales.
