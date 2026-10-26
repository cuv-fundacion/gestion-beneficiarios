# Gestión de Beneficiarios · Cambiando una Vida

Pantalla web de la app de Gestión de Beneficiarios de Fundación Cambiando una Vida A.C.
Se publica en Cloudflare Pages (conectado a este repositorio). Los datos **no** viven aquí: siguen en el Google Sheet "BDD T.S. - SISTEMA"
y en Drive, y los maneja el proyecto de Apps Script (que funciona como servidor).

## Cómo funciona

```
Navegador (tu dominio, Cloudflare)  ──POST {fn, args}──▶  Apps Script /exec (doPost en App_API.gs)
                                 ◀──── JSON ────────   lee/escribe Sheets y Drive
```

- `index.html`: la app completa (es la misma pantalla de `App_Index.html` de Apps Script).
- `config.js`: la URL `/exec` del script. Si se crea una implementación nueva, se cambia aquí.
- `_headers`: encabezados de seguridad para Cloudflare Pages; el sitio no aparece en buscadores.
- `netlify.toml`: lo mismo por si algún día se publica en Netlify.

Este repositorio no guarda datos de niños. No subas exportaciones, capturas reales ni contraseñas.

## Publicar un cambio

1. En Apps Script, edita `App_Index.html` (y los `.gs` que hagan falta) y saca una **Nueva versión**
   de la implementación existente (así la URL no cambia).
2. Genera `index.html` con `build_netlify.py` y súbelo a este repositorio. Cloudflare publica solo.

## Configuración del script (una sola vez)

Implementar → Administrar implementaciones → editar (lápiz):
- Ejecutar como: **Yo**
- Quién tiene acceso: **Cualquier usuario** (sin necesidad de cuenta de Google)

La entrada la protege el usuario + PIN de la app (5 intentos fallidos bloquean 15 minutos).
Solo se pueden llamar las funciones de la lista `APP_API.PERMITIDAS` en `App_API.gs`.
