# Taller interactivo · Entrevista PPI V

Adaptación web del taller **«Del proyecto al guion de entrevista»** para la
Práctica Pedagógica Investigativa V (Licenciatura en Literatura y Lengua
Castellana, Universidad del Magdalena).

- **Página publicada:** <https://samorwno.github.io/taller-entrevista-ppi-v/>
- **Repositorio:** <https://github.com/samorwno/taller-entrevista-ppi-v>
- **Origen:** página estática autocontenida, sin build ni dependencias externas.

## Qué hace

El taller guía ocho etapas: delimitación del proyecto, selección del actor y
cuidado ético, propósito y ejes, preguntas de calidad, diseño del guion,
repreguntas, protocolo de campo y revisión final. Al final permite descargar el
guion en `.doc`, `.txt` o PDF.

Las respuestas se guardan automáticamente en el navegador (`localStorage`) y,
si se configura un token, también pueden guardarse en este repositorio.

## Guardado en GitHub

GitHub Pages es solo estático: no ejecuta código de servidor. Por eso la página
habla **directamente con la API de GitHub** desde el navegador. El token nunca
está en el HTML ni en los respaldos: se guarda únicamente en el `localStorage`
del navegador donde se pega.

### Configurar el token (una vez por navegador)

1. Entra a <https://github.com/settings/personal-access-tokens/new>.
2. Crea un token **fine-grained** con acceso únicamente al repositorio
   `samorwno/taller-entrevista-ppi-v`.
3. En **Repository permissions**, asigna **Contents: Read and write**.
4. Ponle una caducidad razonable y genera el token.
5. En la página, pulsa **Configurar GitHub** (o **Guardar en GitHub**), pega el
   token y guarda.

El token no se puede recuperar después: si se pierde, genera otro y pulsa
**Olvidar token** antes de pegar el nuevo.

### Guardar y cargar

- **Guardar en GitHub** crea o actualiza
  `respuestas/<proyecto-o-equipo>-<id-del-navegador>.json` y hace un commit.
- **Cargar de GitHub** lista los `.json` de `respuestas/` y permite reemplazar
  el avance actual por uno guardado. Leer la lista no requiere token si el
  repositorio es público.
- El botón **Descargar respaldo (.json)** sigue funcionando sin token.

## Estructura

```text
taller-entrevista-ppi-v/
├── index.html          # toda la aplicación (HTML + CSS + JS)
├── .nojekyll           # evita el procesado de Jekyll en GitHub Pages
├── README.md
└── respuestas/         # respuestas guardadas desde la página
    └── README.md
```

Cada archivo de respuesta tiene este formato:

```json
{
  "schema": "ppi-v-respuestas/1",
  "savedAt": "2026-11-11T18:00:00.000Z",
  "deviceId": "a1b2c3",
  "project": "Título del proyecto",
  "team": "Nombre del equipo",
  "state": { "...": "estado completo del taller" }
}
```

El nombre del archivo se deriva del título del proyecto (o del equipo) y de un
identificador aleatorio del navegador. Si cambias el título del proyecto se
creará un archivo nuevo; el anterior permanece en el historial de git.

## Privacidad y seguridad

- El repositorio es **público**: las respuestas guardadas también lo serán. No
  incluyas nombres de estudiantes, documentos, teléfonos ni datos personales.
- El token queda en el `localStorage` del navegador. No lo uses en equipos
  compartidos; si lo haces, pulsa **Olvidar token** al terminar.
- Usa un token fine-grained limitado a este repositorio y con caducidad. No
  pegues un token clásico con permisos amplios.
- Cualquier persona con el token puede escribir en el repositorio. No lo
  publiques ni lo compartas por chat.

## Limitaciones

- No hay backend: si varias personas deben guardar sin configurar un token,
  hace falta un proxy (por ejemplo, una función de Netlify o un Worker de
  Cloudflare) que custodie el token en el servidor. Esa variante no está
  implementada aquí.
- El guardado en GitHub es manual; el guardado local sigue siendo automático.
- La página no envía nada a terceros: solo a `api.github.com` cuando se usa el
  guardado o la carga desde GitHub.

## Desarrollo

No hay build. Para probar localmente:

```bash
cd ~/Work/paginas-web/taller-entrevista-ppi-v
python3 -m http.server 8000
# abrir http://localhost:8000
```

Para publicar, basta con hacer commit y push a `main`; GitHub Pages reconstruye
el sitio automáticamente desde la raíz del repositorio.

## Créditos

Versión beta desarrollada por **Dámar Eduardo Fontalvo Sánchez**. Adaptación
para GitHub Pages con guardado en repositorio.
