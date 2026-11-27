# Tarea 5 — Refactorización CSS de NEXO

## 1. Análisis de los estilos iniciales

Las hojas originales eran `css/claro.css` y `css/oscuro.css`. Ambas utilizaban los mismos selectores:

- `body`
- `header`
- `nav ul`
- `nav ul li`
- `nav ul li a`
- `main`
- `footer`

### Elementos que compartían estilos
La estructura general (tipografía, márgenes, navegación, espaciado y pie) se repetía en los dos temas. Las diferencias entre hojas eran principalmente los colores del encabezado, contenido principal y pie.

### Duplicidades y aspectos mejorables
- Se repetían las reglas estructurales completas en las dos hojas de tema.
- Los enlaces de navegación tenían estilos en CSS y estilos en línea en cada HTML.
- Había estilos en línea para el logotipo, la imagen de portada, el vídeo y la tabla de tarifas.
- Los estilos de tabla se repetían en cada celda mediante atributos `style`.
- Los selectores `nav ul li a` eran más específicos de lo necesario para una navegación que puede resolverse mediante clases.
- No existía un sistema de clases reutilizables para tarjetas, formularios, botones o títulos.

## 2. Creación de clases reutilizables

Se creó `css/base.css` para concentrar la estructura y los componentes compartidos. Entre las clases añadidas están:

- Navegación: `.nav`, `.nav__lista`, `.nav__enlace`.
- Contenido: `.contenido`, `.seccion`, `.titulo`, `.texto-destacado`.
- Tarjetas: `.tarjeta`, `.tarjeta__titulo`, `.tarjeta__texto`.
- Formulario: `.formulario`, `.formulario__grupo`, `.formulario__etiqueta`, `.formulario__campo`.
- Botón: `.boton`.
- Tabla, imágenes y pie: `.tabla-tarifas`, `.imagen-principal`, `.video`, `.pie`.

Las clases se aplican solo a componentes que existen en el sitio. Se eliminaron los estilos en línea de las páginas HTML.

## 3. Aplicación de BEM

Se ha aplicado BEM, al menos, a estos componentes:

**Navegación**
- Bloque: `.nav`
- Elemento: `.nav__lista`, `.nav__enlace`
- Modificador: `.nav__enlace--activo`

**Tarjeta de actividad**
- Bloque: `.tarjeta`
- Elementos: `.tarjeta__titulo`, `.tarjeta__texto`
- Modificador: `.tarjeta--destacada`

También se ha organizado el formulario con el bloque `.formulario` y sus elementos `__grupo`, `__etiqueta` y `__campo`.

## 4. Revisión de especificidad

- Los estilos de componentes se aplican mediante selectores de clase.
- Los identificadores HTML se conservan para identificar secciones y asociar etiquetas de formulario, no para aplicar estilos.
- Se retiraron los estilos en línea.
- No se utiliza `!important`.
- El enlace de la página actual se identifica con `.nav__enlace--activo` y `aria-current="page"`.

## 5. Organización y temas claro/oscuro

La hoja común `base.css` contiene estructura, distribución, componentes y reglas adaptables a pantallas pequeñas. Las hojas `claro.css` y `oscuro.css` contienen únicamente variables y colores del tema.

Todas las páginas cargan primero `base.css`, después el tema claro como hoja preferida y mantienen el tema oscuro como hoja alternativa. Los dos temas definen las mismas variables (`--fondo`, `--superficie`, `--texto`, `--texto-boton`, `--borde` y `--acento`), por lo que los componentes conservan su estructura y cambian de apariencia según el tema.

## Comprobaciones realizadas

- Se han actualizado las cinco páginas HTML.
- Se han eliminado los atributos `style` de las páginas.
- Se mantienen los recursos gráficos y el vídeo originales.
- Se han añadido reglas responsive para navegación, tablas e imágenes.
- El proyecto conserva las dos hojas de tema y añade la hoja común.
