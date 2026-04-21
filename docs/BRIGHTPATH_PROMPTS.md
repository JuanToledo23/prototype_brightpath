# BRIGHTPATH_PROMPTS.md
# 6 prompts autocontenidos para Claude Code — uno por tab
# Usar en orden. Cada prompt agrega un tab al mismo index.html

---

## PROMPT 1 — AUTH (Tab 1)
Copia y pega esto completo en Claude Code

Tienes acceso a dos archivos: `prototype-template.html` y `PROTOTYPE_GUIDE.md`.
Tu tarea: crear `index.html` basado en el template con 6 tabs en el nav.
HOY construyes solo el Tab 1 (Auth) con 3 pantallas. Los otros 5 tabs aparecen en el nav pero vacíos.

### TOKENS CSS BRIGHTPATH — reemplaza el :root completo

```css
:root {
  --brand:#091540; --brand2:#3D518C;
  --accent:#4C9BFD; --accent2:#3a8ae8; --accent-lt:#EBF4FF; --accent-md:#4C9BFD;
  --teal:#46BAB5; --teal-bg:#E6F7F7;
  --coral:#FF6F61; --coral-bg:#FFF0EF;
  --bg:#F2F6FD; --bg2:#E8EEF8;
  --border:#C8D5EC; --border2:#DDE6F5;
  --text:#091540; --text2:#3D518C; --text3:#7A8BB5;
  --green:#059669; --green-bg:#D1FAE5;
  --amber:#D97706; --amber-bg:#FEF3C7;
  --red:#DC2626; --red-bg:#FEE2E2;
  --blue:#4C9BFD; --blue-bg:#EBF4FF;
  --sh:0 1px 3px rgba(9,21,64,.08),0 4px 12px rgba(9,21,64,.04);
  --sh-md:0 4px 16px rgba(9,21,64,.12),0 1px 4px rgba(9,21,64,.06);
  --r:10px; --r-sm:6px; --r-lg:14px;
}
```

Reemplaza el link de Google Fonts:
```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600;700&family=Reddit+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
```

### TOP NAV

```html
<nav class="topnav">
  <div class="brand">
    <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
      <path d="M12 2L14 9L21 7L16 12L21 17L14 15L12 22L10 15L3 17L8 12L3 7L10 9Z" fill="#4C9BFD" opacity="0.9"/>
      <path d="M12 5L13.5 10L19 8.5L15 12L19 15.5L13.5 14L12 19L10.5 14L5 15.5L9 12L5 8.5L10.5 10Z" fill="#FF6F61" opacity="0.6"/>
    </svg>
    <span>BrightPath</span>
    <span style="font-size:10px;font-weight:400;opacity:.5;margin-left:2px">· Prototipo</span>
  </div>
  <button class="stab active" onclick="go('s1')">1 · Auth</button>
  <button class="stab" onclick="go('s4')">2 · Docente</button>
  <button class="stab" onclick="go('s10')">3 · Director</button>
  <button class="stab" onclick="go('s15')">4 · Consultor</button>
  <button class="stab" onclick="go('s19')">5 · Banco de Reactivos</button>
  <button class="stab" onclick="go('s23')">6 · Admin</button>
  <span class="nav-badge">WIREFRAMES v1.0</span>
</nav>
```

### FUNCIÓN go() — reemplaza la del template

```javascript
const tabMap = {
  s1:'t1',s2:'t1',s3:'t1',
  s4:'t2',s5:'t2',s6:'t2',s7:'t2',s8:'t2',s9:'t2',
  s10:'t3',s11:'t3',s12:'t3',s13:'t3',s14:'t3',
  s15:'t4',s16:'t4',s17:'t4',s18:'t4',
  s19:'t5',s20:'t5',s21:'t5',s22:'t5',
  s23:'t6',s24:'t6',s25:'t6',s26:'t6'
};
function go(id) {
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  const el=document.getElementById(id);
  if(el) el.classList.add('active');
  document.querySelectorAll('.stab').forEach(b=>b.classList.remove('active'));
  const tabIdx={'t1':0,'t2':1,'t3':2,'t4':3,'t5':4,'t6':5}[tabMap[id]];
  document.querySelectorAll('.stab')[tabIdx]?.classList.add('active');
  window.scrollTo(0,0);
}
```

### PANTALLAS A CONSTRUIR

**s1 — Login** | scr-label: `🔐 1/3 · Auth` | pg-title: `Inicio de sesión` | burl: `app.brightpath.mx/login`

Anotaciones (4):
1. Fondo degradado Coral→Sky→Deep Horizon comunica transformación y energía de marca BrightPath.
2. Google SSO como opción principal — un click, sin fricción para docentes con cuenta Google.
3. Framing positivo "Tu camino de crecimiento te espera" — nunca lenguaje de examen ni evaluación.
4. Checkbox "Mantener sesión" para docentes en móvil que no quieren hacer login cada vez.

Contenido del .bbody: Fondo linear-gradient(135deg, #FF6F61 0%, #4C9BFD 50%, #091540 100%) padding 40px. Card centrada max-width 420px fondo blanco border-radius 14px padding 32px. Dentro: SVG isotipo + "BrightPath" centrado, H2 "¡Bienvenido de nuevo!", subtítulo "Tu camino de crecimiento te espera", separador, btn-p full-width "🔵 Continuar con Google" → go('s2') + showToast('✓ Autenticando con Google...','ok'), separador "— o —", label+input email placeholder "ejemplo@colegio.edu.mx", label+input password con ojo toggle, row flex justify-between: checkbox "Mantener mi sesión abierta" + link coral "Olvidé mi contraseña", btn-b full-width "Iniciar sesión" → go('s2'), pie centrado "¿No tienes cuenta? " + link accent → go('s3').

**s2 — Selector de Rol** | scr-label: `👋 2/3 · Auth` | pg-title: `¡Bienvenido a BrightPath!` | burl: `app.brightpath.mx/bienvenida`

Anotaciones (4):
1. Este selector SOLO existe en el prototipo — en producción el sistema detecta el rol automáticamente al iniciar sesión.
2. 6 roles con descripción de una línea y CTA directo a la primera pantalla de cada flujo.
3. Coordinador marcado "Próximamente" — rol definido pero no construido en este prototipo.
4. Permite a cualquier validador explorar todas las experiencias sin cuentas separadas.

Contenido: callout-info "Este selector es exclusivo del prototipo. En la app real el sistema detecta tu rol automáticamente." Grid 3 columnas gap 12px con 6 cards: Docente 👩‍🏫 → go('s4'), Director 🏫 → go('s10'), Coordinador 📐 btn-dis "Próximamente", Consultor 👨‍💼 → go('s15'), Experto Reactivos 📝 → go('s19'), Admin ⚙️ → go('s23').

**s3 — Registro** | scr-label: `📝 3/3 · Auth` | pg-title: `Crea tu cuenta` | burl: `app.brightpath.mx/registro`

Anotaciones (4):
1. Google SSO primero — un click para crear cuenta, máxima reducción de fricción.
2. Solo 4 campos si no usa Google — sin formularios que aburren.
3. Tooltip en email explicando beneficio del correo personal sobre el institucional.
4. Checkbox de consentimiento obligatorio — cumplimiento LFPDPPP México.

Contenido: Misma card con fondo degradado. Logo + "Crea tu cuenta" + subtítulo "Tu historial profesional comienza aquí", btn-p Google → go('s2') + toast, separador "— o —", input nombre, input email con ícono ℹ️ tooltip "Usa tu correo personal. Si cambias de colegio tu cuenta te sigue.", input password, input confirmar, checkbox términos, btn-b "Crear cuenta" → go('s2') + showToast('✓ Cuenta creada. ¡Bienvenida!','ok'), pie link → go('s1').

### BOTÓN FLOTANTE Y MODAL FEEDBACK (agregar en todas las pantallas de este tab)

Botón flotante fixed bottom-right:
```html
<button onclick="openModal('modal-feedback')" style="position:fixed;bottom:20px;right:20px;width:48px;height:48px;border-radius:50%;background:var(--accent);color:#fff;border:none;font-size:20px;cursor:pointer;box-shadow:var(--sh-md);z-index:200">💬</button>
```

Modal feedback (agregar UNA VEZ al final del body antes de los scripts):
```html
<div id="modal-feedback" class="modal-ov">
  <div class="modal">
    <div class="modal-title">Enviar Feedback</div>
    <div class="modal-sub">Tu opinión nos ayuda a mejorar BrightPath</div>
    <div style="margin:12px 0"><label class="flbl">Tipo</label>
    <div style="display:flex;gap:12px;flex-wrap:wrap;font-size:12.5px">
      <label><input type="radio" name="fbt" checked> 💡 Feedback</label>
      <label><input type="radio" name="fbt"> 🔧 Bug</label>
      <label><input type="radio" name="fbt"> 💬 Sugerencia</label>
      <label><input type="radio" name="fbt"> ❓ Pregunta</label>
    </div></div>
    <textarea class="ftxt" placeholder="Cuéntanos qué encontraste..." style="margin-bottom:10px"></textarea>
    <div class="callout callout-info" style="font-size:11px;margin-bottom:12px">Se adjuntarán: tu rol, página actual y hora.</div>
    <div class="modal-actions">
      <button class="btn btn-g" onclick="closeModal('modal-feedback')">Cancelar</button>
      <button class="btn btn-p" onclick="closeModal('modal-feedback');showToast('✓ Reporte enviado. Te responderemos pronto.','ok')">Enviar</button>
    </div>
  </div>
</div>
```

### CHECKLIST TAB 1
- [ ] Tokens BrightPath aplicados, DM Sans + Reddit Sans cargados
- [ ] Nav 6 tabs con función go() actualizada
- [ ] s1 s2 s3 con contenido completo y anotaciones
- [ ] Botón 💬 y modal-feedback presentes
- [ ] s1→s2, s3→s2, s2→s4/s10/s15/s19/s23 navegan correctamente
- [ ] Abre sin servidor (file://)

---
---

## PROMPT 2 — DOCENTE (Tab 2)
Al index.html existente (Tab 1 ya construido), agrega Tab 2.
Lee PROTOTYPE_GUIDE.md para instrucciones generales.
NO modifiques s1, s2, s3 ni estilos base.
Agrega pantallas: s4, s5, s6, s7, s8, s9.

Sidebar docente (usar en s4-s9, brand oscuro):
Inicio / Perfil / Mi Diagnóstico / Mis Cursos — Notificaciones / Configuración / Cerrar sesión
El ítem activo cambia según la pantalla.

Datos mock consistentes:
- Docente: Ana Martínez | ana.martinez@gmail.com | Secundaria | 8 años
- Colegio: Colegio Montessori Vallarta
- Scores: MA 72% Profundización | TEC 48% Fundamentos | GSE 85% Implementación | Confianza 91%

**s4 — Onboarding** | scr-label: `👩‍🏫 1/6 · Docente` | pg-title: `¡Hola, Ana Martínez!` | burl: `app.brightpath.mx/bienvenida-docente`
Anotaciones: 1) 3 pasos — mínimo sin saturar. 2) Framing beneficio: "Tu mapa de crecimiento", "Tu portafolio". 3) Email personal con tooltip. 4) Un solo CTA claro.
Layout sb-layout. Contenido: Stepper 3 pasos [1 activo], callout-info bienvenida Colegio Montessori, card "¿Qué es BrightPath para ti?" 4 bullets ✦, card formulario perfil (nombre pre-llenado, email personal tooltip, select nivel, select exp), btn-p → go('s5').

**s5 — Dashboard** | scr-label: `🏠 2/6 · Docente` | pg-title: `Dashboard` | pg-sub: `Hola de nuevo, Ana Martínez 👋` | burl: `app.brightpath.mx/inicio`
Anotaciones: 1) Banner diagnóstico siempre visible al tope. 2) Barra progreso 68% con módulo activo. 3) Métricas de logro positivas. 4) Ruta con estados: En Curso/Próximo/Completado. 5) Sidebar con scores por dimensión.
Layout sb-layout dos columnas 70/30. Col izq: callout-info + btn-p → go('s6'), barra progreso 68% + btn-s → go('s8') + link → go('s7'), mrow 4, 3 cards cursos. Col der: card diagnóstico 3 barras + btn → go('s7'), card próximas, card recursos.

**s6 — Diagnóstico Activo** | scr-label: `📋 3/6 · Docente` | pg-title: `Tu Diagnóstico de Fortalezas` | burl: `app.brightpath.mx/diagnostico/activo`
Anotaciones: 1) Sin cronómetro — sin presión de tiempo. 2) Callout guardado automático elimina ansiedad. 3) Pregunta COMPOSITE: escenario en card azul → sub-preguntas. 4) Círculos Likert 44px táctiles con labels. 5) Botón pausar siempre visible con modal positivo.
IMPORTANTE: NO incluir botón flotante 💬 en esta pantalla.
Contenido: Barra progreso 28% sticky + btn "Pausar" → openModal('modal-pausar'), callout-info guardado, browser chrome, dentro: label coral "Reactivo 3 ─── 28%", card escenario fondo accent-lt (Ana frustrada), sub-pregunta Likert 5 opciones, separador, sub-pregunta múltiple 4 opciones con hover, footer btn-s anterior + btn-p → go('s7').
Modal 'modal-pausar': "¿Pausar diagnóstico?" + info guardado pregunta 8/28 + btn-g Cancelar + btn-p → go('s5') + toast.

**s7 — Resultados** | scr-label: `🎯 4/6 · Docente` | pg-title: `Tu Perfil de Competencias` | burl: `app.brightpath.mx/diagnostico/resultados`
Anotaciones: 1) Callout "Solo tú ves esto" — director en 48h. 2) Niveles cualitativos no solo números. 3) "Fortalezas" y "Áreas de crecimiento" — nunca "deficiencias". 4) Radar SVG 3 dimensiones colores BrightPath. 5) Narrativa IA personalizada para Ana.
Contenido: callout privacidad fondo #F0F9FF, callout-ok diagnóstico 91%, grid 3 cards (MA borde teal / TEC borde coral / GSE borde accent), SVG radar 3 ejes fill accent 0.15, card fortalezas teal-bg, card áreas coral-bg, card narrativa IA bg2, row btns → go('s8') go('s9').

**s8 — Ruta de Formación** | scr-label: `🎓 5/6 · Docente` | pg-title: `Tu Ruta de Formación Personalizada` | burl: `app.brightpath.mx/ruta`
Anotaciones: 1) Generada por diagnóstico — personalizada. 2) Desbloqueo progresivo. 3) Plataformas reconocidas (Google, INTEF, Coursera, edX). 4) Certificado como meta tangible.
Contenido: callout-info, barra progreso 32%, 3 bloques por dimensión con cards recursos (En Curso/Bloqueado/Completado/Disponible), footer card teal certificado.

**s9 — Portafolio** | scr-label: `🌟 6/6 · Docente` | pg-title: `Tu Portafolio Profesional` | burl: `app.brightpath.mx/portafolio`
Anotaciones: 1) Verificado por BrightPath — diferencia del CV tradicional. 2) Link con token único y vigencia. 3) Historial trayectoria — activo más valioso. 4) FutureHiring "Próximamente".
Contenido: header card degradado suave + avatar AM + badge teal verificado, card niveles 3 barras, card timeline 3 filas, card certificados 2 items, card btn-dis oportunidades laborales.
Modal 'modal-compartir': select contexto, select vigencia, preview link, btn copiar → toast.

CHECKLIST TAB 2: s4-s9 completas, s1-s3 intactas, sidebar docente presente, s6 SIN 💬, modal-pausar y modal-compartir funcionando.

---
---

## PROMPT 3 — DIRECTOR (Tab 3)
Al index.html con Tabs 1 y 2, agrega Tab 3.
NO modifiques s1 a s9.
Agrega: s10, s11, s12, s13, s14.

Sidebar director (usar en s10-s14): Dashboard / Mis Docentes / Diagnóstico / Reportes / Re-diagnóstico — Notificaciones / Config.

**s10 — Onboarding** | scr-label: `🏫 1/5 · Director` | pg-title: `¡Bienvenido, Director Ramírez!` | burl: `app.brightpath.mx/director/bienvenida`
Anotaciones: 1) 5 pasos "menos de 10 minutos". 2) Sin selección plan — billing OFF, todos acceden a GUÍA. 3) Teléfono para WhatsApp. 4) Stepper da sensación de control y progreso.
Contenido: sb-layout, stepper 5 pasos [1 activo], card datos (nombre pre-llenado "Colegio Montessori Vallarta", email, tel "+52 322 123 4567", select docentes, select estado "Jalisco", checkboxes niveles), callout-info "Plan activo: GUÍA Completo", btn-p → go('s11').

**s11 — Dashboard Director** | scr-label: `📊 2/5 · Director` | pg-title: `Dashboard Institucional` | burl: `app.brightpath.mx/director`
Anotaciones: 1) Next Actions — qué hacer hoy sin revisar cada sección manualmente. 2) Heatmap semáforo por dimensión/nivel. 3) Tracker con recordatorio WhatsApp en 1 click. 4) Narrativa IA co-branded con logo colegio. 5) Header co-branding BrightPath + Colegio Montessori.
Contenido: header brand blanco "BrightPath | Colegio Montessori Vallarta · Plan GUÍA", callout-warn Next Actions (2 alertas + botones), mrow 4 métricas, card heatmap tabla celdas coloreadas (rojo=Fundamentos, amarillo=Profundización, verde=Implementación), card narrativa IA fondo bg2 borde teal, card completación 5 filas + link → go('s12').

**s12 — Docentes** | scr-label: `👥 3/5 · Director` | pg-title: `Mis Docentes` | burl: `app.brightpath.mx/director/docentes`
Anotaciones: 1) Link WhatsApp más rápido para invitar masivamente. 2) Filtros para encontrar quién falta. 3) Detalle expandible inline al hacer click. 4) Privacidad: solo visible si pasaron 48h desde resultados.
Contenido: toolbar filtros + btn-p "+ Invitar" → openModal('modal-invitar'), mrow 3, tabla 10 docentes + selRow expande detalle.
Modal 'modal-invitar' 3 tabs: "Link único" (btn copiar → toast) | "Lista emails" (textarea) | "CSV" (drop zone).

**s13 — Re-diagnóstico** | scr-label: `🔄 4/5 · Director` | pg-title: `Activar Re-diagnóstico` | burl: `app.brightpath.mx/director/rediagnostico`
Anotaciones: 1) Selección individual o masiva con checkboxes. 2) Fecha límite configurable. 3) WhatsApp automático al activar. 4) Comparativa antes/después automática.
Contenido: callout-info, card selección radios (todos/completados/manual), card config (date, select recordatorios, textarea mensaje), callout-warn WhatsApp, btn-p "Activar para 16 docentes" → openModal('modal-confirm-rediag').
Modal: datos resumen + btn-p → showToast('✓ Re-diagnóstico activado. 16 notificaciones enviadas.','ok') + go('s11').

**s14 — Reportes** | scr-label: `📄 5/5 · Director` | pg-title: `Reportes Institucionales` | burl: `app.brightpath.mx/director/reportes`
Anotaciones: 1) Co-branding automático — director lo comparte como suyo. 2) Solo datos institucionales, privacidad docente protegida. 3) Preview antes de descargar. 4) Comparativa semestral deshabilitada sin re-diagnóstico completado.
Contenido: card tipo reporte (radio 1 y 2, radio 3 btn-dis), select período, btn-p generar → toast, card preview simulada (header co-branded, resumen ejecutivo párrafo, 3 barras tricolor MA/TEC/GSE, footer BrightPath), btn descargar.

CHECKLIST TAB 3: s10-s14 completas, s1-s9 intactas, sidebar director, modales invitar y confirmar funcionando.

---
---

## PROMPT 4 — CONSULTOR & MANAGER (Tab 4)
Al index.html con Tabs 1-3, agrega Tab 4.
NO modifiques s1 a s14.
Agrega: s15, s16, s17, s18.

Sidebar consultor (s15-s18): Mis Colegios / Health Scores / Seguimiento / Tickets.

**s15 — Dashboard Consultor** | scr-label: `👨‍💼 1/4 · Consultor` | pg-title: `Mis Colegios Asignados` | pg-sub: `Lucía Torres · 8 colegios activos` | burl: `app.brightpath.mx/consultor`
Anotaciones: 1) Health Score automático — no subjetivo, calculado por el sistema. 2) Colegios en riesgo al tope — lo más urgente primero. 3) Next Actions sin revisar cada cuenta manualmente. 4) Click en fila va al detalle del colegio.
Contenido: callout-warn 2 alertas (Juárez 18 días / Instituto 3 vencidos), mrow 4 (colegios 8, riesgo 2, docentes 142/180, NPS 8.1), tabla 8 colegios con health scores 🟢🟡🔴, selRow → go('s16').

**s16 — Detalle de Colegio** | scr-label: `🏫 2/4 · Consultor` | pg-title: `Colegio Montessori Vallarta` | burl: `app.brightpath.mx/consultor/colegios/montessori-vallarta`
Anotaciones: 1) Health Score desglosado en componentes (completion, engagement, actividad). 2) Timeline de notas como CRM básico del consultor. 3) 4 acciones rápidas en primera línea. 4) Agregar nota inline sin salir de la pantalla.
Contenido: breadcrumb, header brand + datos, mrow 4 health scores desglosados, row acciones (WhatsApp→toast, registrar nota, agendar, escalar amber), card timeline 3 entradas cronológicas + btn agregar nota, mini tabla 5 docentes.

**s17 — Vista Manager** | scr-label: `📊 3/4 · Manager` | pg-title: `Dashboard Manager` | pg-sub: `Roberto Villanueva · 3 consultores` | burl: `app.brightpath.mx/manager`
Anotaciones: 1) Vista agregada de todos los consultores en un lugar. 2) Comparativa de desempeño sin micro-gestionar. 3) Colegios en riesgo global de los 3 consultores. 4) Sin datos individuales de docentes — solo métricas institucionales.
Contenido: mrow 4 global (colegios 24, riesgo 5, docentes 387, NPS 8.0), tabla comparativa 3 consultores (Lucía 8.4 / Marco 7.8 / Sofía 8.6), card colegios en riesgo tabla 5 + btn notificar → toast.

**s18 — Mis Tickets** | scr-label: `💬 4/4 · Consultor` | pg-title: `Mis Reportes y Feedback` | burl: `app.brightpath.mx/consultor/tickets`
Anotaciones: 1) Comunicación bidireccional — el usuario ve la respuesta del equipo BrightPath. 2) Estados con colores: azul=recibido, amarillo=revisión, verde=resuelto, gris=cerrado. 3) Botón flotante 💬 como entrada principal al feedback. 4) Metadatos de contexto automáticos en cada ticket.
Contenido: callout-info, tabla 4 tickets con estados de color, click "Ver →" en resueltos expande respuesta inline del equipo.

CHECKLIST TAB 4: s15-s18 completas, s1-s14 intactas, tabla s15 clickeable con selRow.

---
---

## PROMPT 5 — BANCO DE REACTIVOS (Tab 5)
Al index.html con Tabs 1-4, agrega Tab 5.
NO modifiques s1 a s18.
Agrega: s19, s20, s21, s22.

Sidebar experto (s19-s22): Dashboard / Banco de Preguntas / Cola RESISTANT / Estado del Banco.

**s19 — Dashboard Banco** | scr-label: `📚 1/4 · Banco de Reactivos` | pg-title: `Banco de Reactivos BrightPath` | pg-sub: `Dr. Carmen Ruiz · QUESTION_EXPERT` | burl: `app.brightpath.mx/reactivos`
Anotaciones: 1) Estado del banco como prioridad visual — qué dimensiones/niveles necesitan atención urgente. 2) Cola RESISTANT (963 pendientes) como acción urgente con callout coral. 3) Corrección ortográfica ya aplicada automáticamente a las 963 preguntas. 4) Semáforos 🔴🟡🟢 por combinación dimensión/nivel.
Contenido: callout coral "963 RESISTANT pendientes de revisión" + btn coral → go('s21'), tabla estado banco con semáforos por dimensión/categoría/nivel, mrow 4 métricas (963 total, 0 RESISTANT aprobadas, 963 corregidas, 2 Impl. cubiertas), row 4 acciones rápidas.

**s20 — Gestión de Preguntas** | scr-label: `📝 2/4 · Banco` | pg-title: `Banco de Preguntas` | burl: `app.brightpath.mx/reactivos/banco`
Anotaciones: 1) Códigos MA-PEDAGOGIAS-FUNDAMENTOS-001 visibles — trazabilidad y referencia. 2) Filtros completos por dimensión/nivel/tipo/estado RESISTANT. 3) Detalle expandible inline con texto completo y opciones. 4) Texto original siempre disponible antes de corrección IA.
Contenido: toolbar filtros + btn-p nueva pregunta, tabla 10 preguntas con códigos reales (usar los del banco: MA-PEDAGOGIAS-FUNDAMENTOS-001, MA-COLABORATIVO-FUNDAMENTOS-021, etc.), selRow expande: texto completo, opciones (correcta marcada ✓), acciones editar/generar RESISTANT.

**s21 — Cola RESISTANT** | scr-label: `🤖 3/4 · Banco` | pg-title: `Cola de Aprobación RESISTANT` | pg-sub: `963 versiones generadas por Claude Sonnet 4.5` | burl: `app.brightpath.mx/reactivos/resistant`
Anotaciones: 1) Comparación lado a lado — original izquierda vs RESISTANT derecha. 2) Razonamiento de la IA explicado en transparencia total. 3) Tres acciones sin ambigüedad: Aprobar/Editar/Rechazar. 4) Sin presión — el banco STANDARD siempre funciona mientras se aprueba.
Contenido: barra progreso "0/963 aprobadas", toolbar con checkbox lote, grid 2 cols (card original fondo bg vs card RESISTANT fondo accent-lt con badge "Claude Sonnet 4.5"), card razonamiento fondo amber-bg, row btns: btn-p "✓ Aprobar" → toast / btn-s "✏ Editar" / btn-d "✗ Rechazar" → openModal('modal-rechazar').
Modal rechazar: radios motivo + btn → toast.

**s22 — Estado del Banco** | scr-label: `📊 4/4 · Banco` | pg-title: `Estado del Banco de Reactivos` | burl: `app.brightpath.mx/reactivos/estado`
Anotaciones: 1) Semáforo verde=suficiente, rojo=crítico para diagnóstico. 2) Números concretos de qué falta y cuánto. 3) Cobertura RESISTANT por dimensión como métrica clave. 4) Guía práctica de prioridades para que el experto sepa en qué enfocarse.
Contenido: mrow 4 (3 en rojo), tabla análisis completo por dimensión/categoría con recomendación por fila, callout-warn 4 recomendaciones priorizadas numeradas (Impl. para MA, banco GSE, aprobar RESISTANT, balancear categorías).

CHECKLIST TAB 5: s19-s22 completas, s1-s18 intactas, grid 2 cols s21 funciona, tabla s20 clickeable.

---
---

## PROMPT 6 — ADMIN (Tab 6) — ÚLTIMO TAB
Al index.html con Tabs 1-5, agrega Tab 6.
NO modifiques s1 a s22.
Este es el último tab — al terminar el prototipo completo estará listo.
Agrega: s23, s24, s25, s26.

Sidebar admin (s23-s26): Dashboard / Tenants (activo en s23) / Usuarios / Tickets / Configuración / Banco Reactivos → go('s19').

**s23 — Panel de Tenants** | scr-label: `⚙️ 1/4 · Admin` | pg-title: `Panel de Administración` | burl: `app.brightpath.mx/admin`
Anotaciones: 1) billing_enabled FALSE visible en callout — no confunde a colegios piloto. 2) Estados con colores: PILOT azul, ACTIVE verde, SUSPENDED amarillo. 3) Activar billing en 1 click + modal de confirmación con advertencia Stripe. 4) Fecha de vencimiento de pilotos para conversión a clientes pagos.
Contenido: callout-info "billing_enabled: FALSE — colegios acceden gratis" + btn-s "Activar billing" → openModal('modal-billing'), mrow 4, tabla 12 tenants con estados de color + btns "Convertir" en pilotos + "Reactivar" en suspendido.
Modal 'modal-billing': advertencia Stripe + btn-d "Activar" → showToast('⚠ Billing activado. Configura Stripe antes de recibir pagos.','ok').

**s24 — Gestión de Usuarios** | scr-label: `👥 2/4 · Admin` | pg-title: `Gestión de Usuarios` | burl: `app.brightpath.mx/admin/usuarios`
Anotaciones: 1) Búsqueda global de cualquier usuario en cualquier colegio. 2) Identidad unificada — emails personal + institucional visibles. 3) Historial de tenants del docente completo. 4) Transferencia preserva historial diagnóstico.
Contenido: toolbar buscar + filtros + btn-p crear, tabla 9 usuarios con roles en badges de colores distintos (TEACHER azul, DIRECTOR amber, CONSULTANT verde, Q_EXPERT indigo, ADMIN rojo), click fila → panel lateral 30% con emails asociados (personal ✓ + institucional), historial tenants, btns transferir y desactivar.

**s25 — Gestión de Tickets** | scr-label: `💬 3/4 · Admin` | pg-title: `Feedback y Soporte` | burl: `app.brightpath.mx/admin/tickets`
Anotaciones: 1) Vista global de todos los tickets de todos los usuarios en la plataforma. 2) BUG primero por impacto en la operación. 3) Respuesta + cambio de estado en una sola acción. 4) Metadatos técnicos (browser, OS, página, timestamp) para diagnosticar bugs sin preguntar más.
Contenido: mrow 3 (abiertos 8 / revisión 3 / resueltos semana 12), tabla 6 tickets con: #, usuario, tipo badge, asunto, rol, página, fecha, estado badge, acción. Click "Responder" expande panel inline con: asunto, metadatos técnicos, textarea respuesta, select estado, btn-p → toast('✓ Respuesta enviada','ok').

**s26 — Configuración Global** | scr-label: `⚙️ 4/4 · Admin` | pg-title: `Configuración Global` | burl: `app.brightpath.mx/admin/config`
Anotaciones: 1) Todos los parámetros del engine adaptativo configurables sin tocar código. 2) Toggles billing/RAG/versionMode con confirmación — cambios de alto impacto controlados. 3) Estado de notificaciones y proveedor Twilio visible con camino a Meta en Fase 2. 4) Parámetros de privacidad y sesiones configurables desde el panel.
Contenido 5 cards:
Card "Billing": toggle OFF + btn activar.
Card "Diagnóstico Adaptativo": tabla 2 cols (Peso LIKERT 0.30 / MULTIPLE 0.50 / COMPOSITE 0.60 / SCENARIO 0.70 / Umbral IMPL ≥0.70 / PROF 0.40-0.69 / FUND <0.40 / Confianza alta ≥0.85 / Tiempo mín escenario 8seg) + btn-s guardar → toast.
Card "Versión de Preguntas": select (STANDARD_ONLY seleccionado) + callout-info sobre RESISTANT.
Card "Validación RAG": toggle OFF + "0 documentos" + btn-dis "Cargar documentos (Próximamente Fase 2)".
Card "Notificaciones": badge bdg-green "Twilio Activo", tabla 5 triggers ✅, btn-dis "Migrar a Meta (Próximamente Fase 2)".
Card "Sesiones": 4 parámetros de texto + btn-s solicitudes LFPDPPP → toast.

### CHECKLIST FINAL COMPLETO

- [ ] Los 6 tabs navegan correctamente desde el nav
- [ ] 26 pantallas con contenido real y datos coherentes
- [ ] Todas las ann-panel con 4+ items descriptivos
- [ ] Botón flotante 💬 en todas las pantallas EXCEPTO s6
- [ ] s6 (diagnóstico activo) NO tiene botón flotante
- [ ] Funcionalidades futuras: btn-dis + badge "Próximamente"
- [ ] Datos consistentes en todo el prototipo: Ana Martínez / Colegio Montessori Vallarta / Lucía Torres / Dr. Carmen Ruiz
- [ ] Framing correcto: "diagnóstico de fortalezas", "perfil de competencias" — nunca "evaluación" ni "examen"
- [ ] Sin errores en consola del browser
- [ ] Abre directamente desde file:// sin servidor
- [ ] Nombre del archivo: index.html
