# Control de Campaña

Plataforma de trabajo territorial electoral: consulta del padrón, organización del
equipo de campaña por área y nivel de candidato, seguimiento de campo y mapas de
circuitos, distritos y corregimientos.

## Qué incluye

- **Padrón** — búsqueda por cédula, nombre o apellido; filtros por corregimiento,
  mesa, partido y estado. (Datos cargados: los 5 corregimientos del distrito de
  Gualaca, Chiriquí — 8,389 electores del padrón oficial del Tribunal Electoral,
  edición 5 de mayo de 2024. La estructura soporta el resto del país.)
- **Afiliación e inscripción a partido** y **depuración de campo** (fallecido, no
  vive en el lugar, cambio de residencia), teléfono y ubicación GPS por persona.
- **Mapa y ruta** — pines por partido/estado, ruta de recorrido, buscador de
  lugares, y visualización recortada de cualquier **circuito electoral (39)**,
  **distrito** o **corregimiento** del país, con exportación a PDF.
- **Administración** (solo rol admin) — crear cuentas de colaboradores limitadas a
  las áreas que les corresponden según su nivel (presidente, diputado, alcalde,
  representante, secretaría de organización) y carga masiva por Excel/CSV.

## Uso local

```bash
python -m http.server 8000
```

y visita `http://localhost:8000` (con `?v=<n>` para saltar la caché al probar cambios).

## Agregar colaboradores

Desde la app: pestaña **⚙️ Administración → Crear cuenta de colaborador**. Se elige el
nivel del candidato y el área permitida; se genera una contraseña temporal para
compartir. El registro público está desactivado.

## Stack

- **Base de datos:** Supabase (PostgreSQL) con Row Level Security por área y
  búsqueda de texto completo en español.
- **Frontend:** HTML + JS estático (sin build). `@supabase/supabase-js`, Leaflet y
  jsPDF vía CDN.
- **Autenticación:** Supabase Auth (email + contraseña). Creación de cuentas por
  Edge Function con verificación de rol admin.
- **Datos geográficos:** circuitos (Ley 299 de 5/5/2022) y límites de
  distritos/corregimientos derivados del dato oficial STRI 2022, en `circuitos/` y
  `distritos/`.
