# Padrón Electoral — Distrito de Gualaca

Sistema de consulta del padrón electoral de los 5 corregimientos del distrito de Gualaca, Chiriquí, Panamá (Cabecera, Hornito, Los Ángeles, Paja de Sombrero, Rincón).

- **8,389 electores** cargados desde el padrón fotográfico oficial del Tribunal Electoral (edición 5 de mayo de 2024).
- Búsqueda por cédula, nombre o apellido.
- Filtros por corregimiento y mesa.
- Acceso protegido: solo usuarios con cuenta autorizada pueden consultar.

## Uso local

Abre `index.html` directamente en el navegador, o sirve la carpeta con:

```bash
python -m http.server 8000
```

y visita `http://localhost:8000`.

## Cómo agregar una persona del equipo

1. Ve al [panel de Supabase → Authentication → Users](https://supabase.com/dashboard/project/ydedoolppdjyzxweqcex/auth/users)
2. Click **Add user → Create new user**
3. Ingresa su correo y una contraseña temporal, marca **Auto Confirm User**
4. Comparte esas credenciales con la persona

El registro público está desactivado — solo el administrador puede dar de alta cuentas nuevas.

## Stack

- **Base de datos:** Supabase (PostgreSQL) con Row Level Security y búsqueda de texto completo en español
- **Frontend:** HTML + JS estático (sin build), usando `@supabase/supabase-js` vía CDN
- **Autenticación:** Supabase Auth (email + contraseña)
