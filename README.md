# Mallas FEN — malla curricular interactiva

Web interactiva (un solo HTML + data.js) con las mallas de las carreras de FEN,
Universidad de Chile: **Ingeniería Comercial** (Lic. Administración y Lic. Economía),
**Contador Auditor** e **Ingeniería en Información y Control de Gestión** — cada una
con su **Malla 2026** y su **malla anterior** (8 mallas en total).

## Funciones
- Marca ramos como *cursando* o *aprobado* (se guarda en tu navegador, por malla).
- Prerrequisitos reales extraídos de las flechas de los PDF oficiales: los ramos
  se bloquean/desbloquean según tu avance.
- Al tocar un ramo se ilumina su **cadena**: prerrequisitos (ámbar) y lo que abre (verde).
- Umbrales de créditos de las notas al pie (120/150/180/220/240) como requisitos
  y como marcas en el termómetro de avance.
- Vías del ciclo profesional en Ing. Comercial (Magíster vs Práctica Profesional).
- Carga estimada: cada crédito ≈ 1,5 h de estudio semanal fuera de cátedra.
- Exportar / importar avance en JSON.
- **Onboarding**: al entrar por primera vez eliges en qué semestre vas y se marca
  todo lo anterior de una pasada (botón «Avance rápido» para repetirlo).
- **Flechas reales**: al seleccionar un ramo se dibujan en SVG las flechas de su
  cadena de prerrequisitos (ámbar) y de los ramos que abre (verde).
- **🧮 Calculadora de nota**: pondera evaluaciones (nombre · % · nota) al estilo FEN
  (el examen es una nota más del promedio). Deja una evaluación en blanco y despeja
  la nota que necesitas para tu meta (4,0 por defecto, editable). Presets de evaluación,
  autocompleta el % de la evaluación que dejes en blanco (si el resto suma <100),
  y un requisito extra configurable (nota mínima en el examen, o promedio simple/ponderado
  entre evaluaciones ≥ X): la nota que te pide es la mayor entre el 4,0 general y ese requisito. Disponible como
  herramienta suelta (botón en la barra) y dentro de cada ramo, guardándose junto al avance.
- **🗓️ Próximo semestre**: lista los ramos que ya tienes habilitados (prerrequisitos
  y créditos cumplidos) y te deja armar una carga tentativa viendo créditos y horas de estudio.
- **🎓 Simular egreso**: eliges cuántos créditos tomas por semestre y proyecta en cuántos
  semestres terminas, respetando prerrequisitos, con el desglose de carga por semestre.

- **Buscador** de ramos (Enter selecciona el primero) y **notas** por ramo con
  PPA ponderado por créditos.
- **Compartir como imagen**: botón 📷 en la malla, la calculadora, el planificador y el
  simulador. Genera un PNG (con encabezado de carrera y avance) para descargar o copiar al
  portapapeles. Usa html2canvas desde CDN.
- **Compartir por URL**: tu avance también viaja codificado en el enlace (~40 caracteres),
  sin backend ni cuentas.

## Archivos
- `index.html` — la app completa (incluye la pantalla de bienvenida y meta tags Open Graph).
- `data.js` — las 8 mallas.
- `og.png` — imagen de previsualización al compartir el enlace (1200×630). Debe ir junto al index.

## Deploy
- **Netlify**: arrastra la carpeta (o solo `index.html` + `data.js`) a app.netlify.com/drop.
- **GitHub Pages**: push del repo → Settings → Pages → rama main.

## Regenerar los datos
Los PDFs originales no se incluyen. Con ellos en `uploads/`:
```
python3 tools/extract_old.py   # mallas antiguas (texto extraíble)
python3 tools/extract_new.py   # mallas 2026 (geometría vectorial)
python3 tools/curate.py        # produce data/*.json finales
```
Las flechas se extraen de los paths vectoriales del PDF y su dirección se valida
con las puntas de flecha; los nombres de las mallas 2026 se etiquetaron
manualmente (`tools/labels_new.py`) verificados por posición, color y tamaño.

## Disclaimer
Proyecto no oficial. Verifica siempre tu situación curricular con la
Secretaría de Estudios de FEN.
