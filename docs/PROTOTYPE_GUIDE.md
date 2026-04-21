# PROTOTYPE_GUIDE.md
# Instrucciones para Claude Code: generar prototipos interactivos

---

## Tu tarea

Cuando recibas un documento de producto, genera un prototipo HTML interactivo.
El resultado es **un solo archivo HTML** basado en `prototype-template.html`.
Funciona abriéndolo directamente en el navegador, sin servidor, sin dependencias.

---

## Antes de escribir código: lee y extrae

1. ¿Qué es el producto/funcionalidad? ¿Para quién?
2. ¿Cuál es el flujo del usuario de principio a fin?
3. ¿Cuántas pantallas necesita? Una por paso importante del flujo. Máximo 6.
4. ¿Qué datos de ejemplo hay en el documento? Úsalos exactamente.
5. ¿Qué está fuera de alcance (v1.1, futuro)? Márcalo como deshabilitado.

---

## Cómo generar el prototipo

**Copia `prototype-template.html`** y modifícalo:

### 1. Top Nav
Cambia el nombre de la marca y agrega un `<button class="stab">` por cada pantalla del flujo.
El orden de los tabs = orden del flujo del usuario.

### 2. Pantallas
Duplica el bloque `<div id="s1" class="screen active">` para cada pantalla.
- Cambia `s1` por `s2`, `s3`, etc.
- Actualiza `scr-label`, `pg-title`, `pg-sub`
- Llena el contenido dentro del `.bbody`
- Agrega el `onclick="go('sN')"` correcto a los botones de navegación

### 3. Panel de anotaciones
Cada pantalla necesita un `.ann-panel` con mínimo 3 `.ann-item`.
Anota los elementos más importantes o menos obvios de cada pantalla.

### 4. Marcadores numéricos
Coloca `.ann-mk` con `data-tip="..."` junto a los elementos anotados.
El número del marcador debe coincidir con el número en el `.ann-panel`.

```html
<div style="position:relative; display:inline-block;">
  <div class="ann-mk" data-tip="Explicación aquí" style="top:-9px; right:-9px;">1</div>
  <!-- el elemento que se anota -->
</div>
```

---

## Componentes disponibles en el template

Úsalos — no inventes CSS nuevo:

| Para mostrar... | Usa... |
|---|---|
| Sección delimitada | `.card` + `.card-head` + `.card-body` |
| Filtros + contenido principal | `.sb-layout` + `.sidebar` + `.main-col` |
| Lista de datos con columnas | `.tbl` |
| Números importantes | `.mrow` + `.mc` |
| Confirmación o alerta | `.callout-ok` / `.callout-warn` / `.callout-info` |
| Sin datos todavía | `.empty-state` |
| Flujo de confirmación | `.modal-ov` + `.modal` |
| Carga en progreso | `showSkeleton('id', N)` |
| Estado "no disponible aún" | `.btn-dis` + badge `.bdg-gray` + texto "Próximamente" |
| Etiqueta de estado | `.badge .bdg-green` / `.bdg-amber` / `.bdg-red` / `.bdg-blue` |
| Valor del modelo ML | `.ind-hi` / `.ind-md` / `.ind-lo` (Alto/Medio/Bajo) |
| Elemento seleccionable | `.chip` |

**Para colores, usa siempre las variables CSS:**
`var(--brand)` `var(--accent)` `var(--accent-lt)` `var(--text)` `var(--text2)` `var(--text3)` `var(--bg)` `var(--bg2)`

---

## Funciones JS disponibles

```javascript
go('s2')                          // navegar a pantalla s2
openModal('modal-id')             // abrir modal
closeModal('modal-id')            // cerrar modal
showToast('✓ Guardado', 'ok')     // toast verde
showToast('Error al guardar', 'err') // toast rojo
showToast('Procesando...')        // toast neutro
selRow(rowEl, callback)           // seleccionar fila de tabla
showSkeleton('container-id', 5)   // skeleton loading (N filas)
```

---

## Interactividad mínima obligatoria

- Los botones principales navegan a la pantalla siguiente del flujo
- Siempre hay forma de volver a la pantalla anterior
- Si hay tabla: las filas son clickeables y algo cambia al seleccionar
- Botones que necesitan acción previa empiezan como `.btn-dis` y se activan con JS
- Al menos una confirmación modal o un toast en el flujo
- Después de guardar/confirmar: `showToast('✓ Mensaje', 'ok')`

---

## Datos de ejemplo

- Usa datos realistas del dominio del producto, nunca "Lorem ipsum" ni "Item 1"
- Si el documento tiene datos específicos (nombres, números, fechas), úsalos exactamente
- Mínimo 3 filas en tablas
- Los números deben ser coherentes entre pantallas

---

## Cambiar la identidad visual

Si el proyecto tiene colores distintos, solo edita las variables en `:root` al inicio del CSS.
No toques nada más.

---

## Checklist antes de entregar

- [ ] Todas las pantallas tienen contenido
- [ ] Todas tienen `.ann-panel` con mínimo 3 items
- [ ] Todos los `.ann-mk` tienen `data-tip` con texto descriptivo
- [ ] Los botones de navegación llevan al flujo correcto
- [ ] Al menos un modal o toast funcional
- [ ] Datos coherentes entre pantallas
- [ ] Funcionalidades futuras marcadas con "Próximamente"
- [ ] Sin errores en consola del browser
- [ ] Abre sin servidor (file://)

---

## Nombre del archivo de salida

`prototype-[nombre-del-proyecto].html`
