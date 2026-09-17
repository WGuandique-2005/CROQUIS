# 🗺️ Croquis — Editor de Planos y Campus

**Croquis** es una aplicación web interactiva, ligera y autónoma diseñada para la delimitación, edición y diseño vectorial de planos de campus, complejos deportivos, recintos educativos e instalaciones arquitectónicas. 

Desarrollado exclusivamente con tecnologías web nativas (**HTML5**, **CSS3**, **Vanilla JavaScript** y gráficos vectoriales **SVG**), funciona directamente en cualquier navegador web sin requerir instalaciones, dependencias externas complejas ni procesos de compilación (*zero-build*).

---

## 🚀 Características Principales

### 📐 1. Delimitación y Geometría Vectorial Libre
* **Límite perimetral del terreno:** Permite definir el contorno del campus mediante polígonos editables vértice a vértice, calculando automáticamente perímetro ($m$) y área total ($\approx m^2$).
* **Dibujo vértice a vértice (`P`):** Creación precisa de polígonos personalizados haciendo clic para colocar puntos y cerrando con `Enter` o doble clic.
* **Trazo libre a mano alzada (`F`):** Dibujo continuo de zonas que se simplifica y suaviza automáticamente mediante el algoritmo matemático **Douglas-Peucker**.
* **Edición interactiva de vértices:** Manipulación en tiempo real de nodos, inserción de vértices en los puntos medios (`◇`) y eliminación precisa (`Alt + Clic` o tecla `Supr`).

### 🏛️ 2. Sellos y Tipologías de Zonas Predefinidas
Incluye sellos paramétricos con estilos arquitectónicos y patrones gráficos vectoriales únicos:
* **Edificios (`B`):** Estructura arquitectónica con achurado interno y contorno de muros.
* **Auditorios (`A`):** Distribución de escenario, gradas y butacas radiales estilizadas.
* **Canchas Deportivas (`C`):** Campo de juego reglamentario con césped rayado, círculo central, áreas de meta y porterías.
* **Estacionamientos (`E`):** Carriles de circulación, cajones de aparcamiento, flechas de tráfico y vehículos generados proceduralmente.
* **Plazas / Glorietas (`G`):** Suelos adoquinados, fuentes o monumentos centrales, bancas de descanso y jardinería periférica.

### 🌳 3. Sistema de Vegetación Procedural
* **Pincel de Vegetación (`N`):** Coloca árboles dispersos dinámicamente arrastrando el ratón sobre el plano, con variaciones de tono y tamaño configurable.
* **Borrador de Vegetación (`X`):** Radio circular de borrado para remover árboles de forma no destructiva sin alterar los polígonos de las edificaciones ni el terreno.

### ⚙️ 4. Transformación y Edición Detallada
* **Manipulación total:** Traslación, escalado multidireccional desde las esquinas y rotación libre mediante la manija superior `R` (con ajuste a intervalos de 15° manteniendo presionada la tecla `Shift`).
* **Panel de atributos:** Personalización de código/sigla (ej. *HL*, *CD*, *AU*), nombre, tipo de zona, descripción enriquecida, opacidad y paleta cromática (o selector de color nativo).
* **Gestión de capas:** Traer al frente, enviar al fondo, duplicar elementos, alternar visibilidad (mostrar/ocultar) y bloqueo de seguridad (*candado*) para proteger contornos y ubicaciones contra movimientos accidentales.

### 📄 5. Exportación de Alta Fidelidad (Desde Datos Vectoriales)
A diferencia de capturas de pantalla convencionales, el motor de exportación reconstruye una imagen vectorial nítida desde el estado matemático del proyecto:
* **Encuadre automático:** Detecta el *bounding box* de todos los elementos presentes (campus, edificaciones y vegetación) para que ningún objeto quede recortado, sin importar el nivel de zoom actual.
* **Exportación PNG (3200 px):** Renderizado en ultra alta resolución acompañado de cartela técnica profesional, leyenda de colores, fecha de generación y metadatos de autor.
* **Exportación PDF Multipágina (jsPDF):**
  * **Página 1:** Plano general en orientación horizontal (A4) con marco arquitectónico, cartela, leyenda y estadísticas.
  * **Páginas siguientes:** Tabla formal de *Registro de Zonas* con código, nombre, categoría, superficie calculada en $m^2$ y descripción detallada de cada espacio.
  * **Vista previa interactiva:** Ventana modal de previsualización antes de confirmar la descarga.

### 💾 6. Persistencia y Portabilidad
* **Autoguardado Local:** Guarda automáticamente cada cambio en `localStorage` con historial de deshacer/rehacer (**Undo** con `Ctrl + Z` hasta 40 pasos).
* **Importación y Exportación JSON:** Respaldo completo de la estructura del plano en archivos `.json` compatibles para compartir, versionar o migrar proyectos.
* **Modo Presentación:** Oculta paneles, barras de herramientas y menús para proyectar o visualizar el plano a pantalla completa en reuniones o exhibiciones.

---

## ⌨️ Atajos de Teclado

| Tecla | Acción |
| :---: | :--- |
| <kbd>V</kbd> | Herramienta de selección (mover, escalar, rotar y editar vértices) |
| <kbd>P</kbd> | Dibujar zona poligonal punto a punto |
| <kbd>F</kbd> | Dibujar zona a mano alzada (trazo libre) |
| <kbd>T</kbd> | Redibujar el límite perimetral del campus |
| <kbd>B</kbd> | Colocar sello de **Edificio** |
| <kbd>A</kbd> | Colocar sello de **Auditorio** |
| <kbd>C</kbd> | Colocar sello de **Cancha deportiva** |
| <kbd>E</kbd> | Colocar sello de **Estacionamiento** |
| <kbd>G</kbd> | Colocar sello de **Plaza / Glorieta** |
| <kbd>N</kbd> | Pincel de vegetación (plantar árboles) |
| <kbd>X</kbd> | Goma de vegetación (borrar árboles) |
| <kbd>R</kbd> | Rotar la zona seleccionada 90° en sentido horario |
| <kbd>Enter</kbd> | Cerrar y finalizar el polígono en curso |
| <kbd>Backspace</kbd> / <kbd>Supr</kbd> | Eliminar el último vértice dibujado o borrar la zona seleccionada |
| <kbd>Ctrl + Z</kbd> | Deshacer la última acción |
| <kbd>Esc</kbd> | Cancelar herramienta activa / Deseleccionar / Salir de presentación |

---

## 🛠️ Tecnologías y Fundamentos Matemáticos

* **Frontend:** HTML5 semántico, CSS3 moderno (Variables CSS, CSS Grid, Flexbox).
* **Gráficos:** SVG (*Scalable Vector Graphics*) nativo en el DOM, `<pattern>`, `<clipPath>`, transformaciones afines y renderizado dinámico en `<canvas>`.
* **Tipografía:** [Archivo](https://fonts.google.com/specimen/Archivo) e [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono).
* **Librerías externas:** [jsPDF v2.5.1](https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js) (CDN para compilación de documentos PDF).
* **Algoritmos implementados en JavaScript:**
  * **Fórmula de Gauss / Área de Lazar (Shoelace formula):** Cálculo exacto del área de polígonos irregulares.
  * **Cálculo de Centroides Poligonales:** Posicionamiento automático y centrado de etiquetas de texto sobre cada zona.
  * **Douglas-Peucker:** Reducción de puntos y optimización de curvas en el trazo libre.
  * **Point-in-Polygon (Ray Casting):** Detección de colisiones e inclusión de puntos dentro de polígonos.
  * **Mulberry32 & FNV/djb2 Hashing:** Generador pseudoaleatorio basado en semillas fijas para recrear patrones idénticos (ej. distribución de vehículos en estacionamientos).

---

## 📁 Estructura del Repositorio

```text
CROQUIS/
├── croquis.html             # Aplicación completa (HTML, CSS y JavaScript integrados)
├── croquis-campus.json      # Archivo de datos de ejemplo (exportación en formato JSON)
├── croquis-campus-UGB.pdf   # Ejemplo del PDF generado con el croquis y registro de zonas
└── README.md                # Documentación del proyecto
```

---

## 🖥️ Cómo Ejecutar el Proyecto

No se requieren herramientas de construcción (*bundlers* como Webpack o Vite) ni servidores de Node.js.

### Opción 1: Apertura Directa
1. Haz doble clic sobre el archivo `croquis.html` o arrástralo directamente a cualquier navegador web moderno (Google Chrome, Mozilla Firefox, Microsoft Edge, Safari, Brave).

### Opción 2: Mediante un Servidor Local Ligero (Opcional)
Si deseas servir el proyecto a través de HTTP/HTTPS local:

* **Con Python 3:**
  ```bash
  python3 -m http.server 8000
  ```
  Abre en tu navegador `http://localhost:8000/croquis.html`.

* **Con Node.js (npx serve):**
  ```bash
  npx serve .
  ```

---

## 📊 Estructura de Datos (JSON)

Al exportar mediante el menú **Datos > Exportar JSON**, se produce un archivo estructurado con la siguiente especificación:

```json
{
  "version": 4,
  "terrain": {
    "name": "Campus",
    "points": [
      { "x": 200, "y": 160 },
      { "x": 560, "y": 110 }
    ]
  },
  "items": [
    {
      "id": "z_abc123",
      "kind": "bldg",
      "code": "HL",
      "name": "Edificio Hugo Lindo",
      "desc": "Aulas de Ingeniería y Sistemas.",
      "color": "#D97B2F",
      "visible": true,
      "locked": false,
      "rot": 0,
      "opacity": 0.24,
      "poly": [
        { "x": 250, "y": 185 },
        { "x": 560, "y": 185 },
        { "x": 560, "y": 300 },
        { "x": 250, "y": 300 }
      ]
    }
  ],
  "trees": [
    { "x": 420, "y": 310, "r": 9, "tone": 0.65 }
  ],
  "doc": {
    "title": "Croquis del campus",
    "subtitle": "Plano de delimitación libre",
    "author": "Universidad",
    "labelMode": "full",
    "showArea": false,
    "snap": false,
    "grid": false,
    "brushR": 9,
    "eraserR": 36
  }
}
```

---

## 📜 Licencia

Distribuido para uso libre en la planificación, edición y presentación de planos educativos e institucionales.
