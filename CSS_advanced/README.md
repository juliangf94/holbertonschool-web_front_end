# Holberton School - CSS Advanced

Este proyecto representa la culminación del módulo de **CSS Avanzado** en Holberton School (Rennes). A lo largo de 32 tareas incrementales, he desarrollado un framework de estilos robusto, escalable y dinámico, aplicando las mejores prácticas de arquitectura CSS y diseño de interfaces interactivas.

## 🚀 Resumen del Proyecto

El objetivo fue transformar una estructura HTML base en una experiencia de usuario (UX) moderna y fluida. El proyecto se centra en el uso de variables dinámicas, sistemas de grillas manuales, y animaciones avanzadas para crear un sitio web profesional y visualmente impactante.

## 🛠️ Conceptos Técnicos Aplicados

* **Arquitectura Modular**: Organización del código en secciones lógicas (Variables, Base Styles, Layout, Components y Themes).
* **Custom Properties (Variables CSS)**: Uso de `:root` para centralizar colores, tipografías y tiempos de transición, facilitando el mantenimiento global.
* **Pseudoelementos (`::before`, `::after`)**:
    * Creación de efectos de subrayado animados en la navegación.
    * Inserción de comillas decorativas tipográficas (`\201C`) en testimonios.
    * Creación de áreas cliqueables extendidas en tarjetas de trabajo.
* **Animaciones y Microinteracciones**:
    * Uso de `cubic-bezier` para transiciones más naturales y elásticas.
    * Efectos de hover complejos con `transform: scale()` y cambios de opacidad.
* **Optimización Visual**: Implementación de `object-fit: cover` para asegurar la consistencia de las imágenes en toda la plataforma.

## 📂 Estructura del Repositorio

| Directorio | Archivo | Descripción |
| :--- | :--- | :--- |
| `CSS_advanced` | `index.html` | Estructura principal del sitio. |
| `CSS_advanced/styles/` | `32-style.css` | Archivo final con la implementación completa de las 32 tareas. |

## 💡 Destacados del Código

### Efecto de Zoom y Contenedor (Task 30 & 32)
Se implementó un efecto de "lupa inversa" donde el contenedor se encoge mientras la imagen se expande al hacer hover:
```css
.card-work:hover .card-outer { transform: scale(0.95); }
.card-work:hover .card-image img { transform: scale(1.2); }
```
## Navegación Dinámica (Task 29 & 32)
Los enlaces de navegación cuentan con una barra superior decorativa que se expande desde el centro con una transición fluida:

```CSS
.nav .nav-link::before {
  transition: var(--transition-duration) var(--transition-cubic-bezier);
  width: 0;
}
.nav .nav-item:hover .nav-link::before { width: 100%; }
```
**Alumno**: Julian Gonzalez

**Cohorte**: Holberton School, Rennes

