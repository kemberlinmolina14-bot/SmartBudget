# SmartBudget — Documentación y Justificación Metodológica

Este documento detalla las decisiones arquitectónicas, metodológicas y de diseño de interfaz implementadas para el desarrollo de la Landing Page de **SmartBudget**, correspondiente a la evaluación práctica del Módulo 3.

---

## 1. Arquitectura de Estilos y Uso de SASS
Para asegurar un código escalable, mantenible y limpio, se implementó **SASS/SCSS** siguiendo una versión simplificada de la arquitectura **7-1 Pattern**:

*   **`abstracts/`**: Contiene las variables globales (`_variables.scss`) que centralizan la paleta de colores y espaciados, junto con los mixins (`_mixins.scss`) encargados de gestionar los breakpoints de responsividad.
*   **`base/`**: Define las reglas globales de reseteo (`_reset.scss`) usando `box-sizing: border-box`, asegurando consistencia matemática en el modelo de cajas, además de la gestión de fuentes (`_typography.scss`).
*   **`components/`**: Módulos aislados y reutilizables como botones (`_buttons.scss`), tarjetas decorativas (`_cards.scss`) y el cuadro de diálogo interactivo (`_modals.scss`).
*   **`layout/`**: Se encarga de las grandes macro-secciones del sitio como la barra de navegación (`_navbar.scss`), el bloque de bienvenida (`_hero.scss`) y el pie de página (`_footer.scss`).

Todos estos archivos parciales (*partials*) inician su nomenclatura con un guion bajo (`_`) y son unificados jerárquicamente en el archivo central `main.scss`, compilando una única hoja de estilos optimizada en `css/main.css`.

---

## 2. Metodología CSS: BEM (Block, Element, Modifier)
Se optó por la metodología **BEM** combinada con un prefijo de proyecto personalizado (`sb-`) para evitar colisiones con clases nativas del navegador o de librerías externas:

*   **Bloque**: `.sb-card` (Representa la entidad autónoma de la tarjeta de beneficios).
*   **Elemento**: `.sb-card__title` (Depende semánticamente de la tarjeta y hereda sus estilos base).
*   **Modificador**: `.sb-btn--primary` (Altera el estado visual o el esquema de color del botón).

Esta nomenclatura garantiza el aislamiento de estilos y elimina por completo el acoplamiento directo a etiquetas HTML, facilitando futuras refactorizaciones.

---

## 3. Integración de Bootstrap 4 y Diseño Responsivo
El proyecto aprovecha las fortalezas de **Bootstrap 4** en perfecta sinergia con estilos personalizados:

*   **Estructura Semántica**: Se implementó un flujo HTML5 nativo mediante el uso estricto de `<header>`, `<main>`, `<section>` y `<footer>`.
*   **Grilla y Flexbox**: Se utilizó el sistema de filas (`row`) y columnas (`col-md-6`, `col-md-4`) de Bootstrap para lograr una distribución fluida. Las tarjetas adaptan su altura de forma idéntica mediante Flexbox para resguardar la armonía visual.
*   **Responsividad**: El comportamiento se adaptó minuciosamente para tres entornos clave:
    1.  *Desktop*: Visualización en columnas paralelas con amplios espacios en blanco.
    2.  *Tablet*: Reacomodo de grillas para prevenir textos colapsados.
    3.  *Mobile*: Menú de navegación colapsable nativo y apilamiento vertical fluido de los elementos para una lectura natural.
*   **Componentes Interactivos**: El acceso a la plataforma simula un entorno dinámico real utilizando el componente **Modal de Bootstrap**, acoplado mediante atributos declarativos (`data-toggle="modal"`), evitando la inyección innecesaria de scripts personalizados.