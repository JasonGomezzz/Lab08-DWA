# Lab08-DWA · Despliegue de aplicaciones con JWT

Laboratorio 08 de Desarrollo de Aplicaciones Web Avanzado (TECSUP). Despliega en la nube el proyecto del Laboratorio 07 (API con JWT, roles y frontend EJS): base de datos en MongoDB Atlas, API en Render y despliegue continuo con GitHub Actions.

| Pieza | Servicio |
|---|---|
| Código | Carpeta [`express-auth/`](express-auth) |
| Base de datos | MongoDB Atlas (cluster gratuito) |
| API | Render, plan Free, servicio `express-auth-<apellido>` |
| CI/CD | GitHub Actions: [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) |

La instalación, las variables de entorno, los endpoints y el despliegue paso a paso están en el [README de `express-auth`](express-auth/README.md).

## Pipeline de CI/CD

1. Un push a `main` que modifique `express-auth/` (o una ejecución manual) dispara el workflow.
2. El job `test` instala dependencias con `npm ci` y corre `npm test`.
3. Si las pruebas pasan, el job `deploy` hace `POST` al Deploy Hook de Render, que publica el último commit.

## Seguridad

- Las credenciales de Atlas y las claves JWT viven solo en `.env` (local) y en las variables de entorno de Render. En el repositorio solo hay `.env.example` con valores de ejemplo.
- El Deploy Hook es un secret de GitHub Actions (`RENDER_DEPLOY_HOOK_URL`); nunca se escribe en el código.
