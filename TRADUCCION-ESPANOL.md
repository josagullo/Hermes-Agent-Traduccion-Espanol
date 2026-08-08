# Traducción al Español — Hermes Agent

Este fork mantiene la **traducción completa al español** de Hermes Agent para la
comunidad hispanohablante.

## Qué está traducido

| Componente | Archivo | Estado |
|------------|---------|--------|
| Documentación principal | `README.es.md` | ✅ Completo |
| Guía de contribución | `CONTRIBUTING.es.md` | ✅ Completo (1:1 con la versión en inglés) |
| Política de seguridad | `SECURITY.es.md` | ✅ Completo |
| Catálogo de la UI del agente | `locales/es.yaml` | ✅ Completo (394/394 claves) |
| **Interfaz de escritorio (Desktop)** | `apps/desktop/src/i18n/es.ts` | ✅ Añadido y registrado |

## Cómo activar el español en tu instalación

### Interfaz de escritorio (Hermes Desktop)
1. Abre **Hermes Desktop**.
2. En la **barra lateral izquierda, abajo** (junto al icono de tema sol/luna),
   haz clic en el selector de idioma.
3. Elige **"Español"**. La elección se guarda automáticamente.

> El selector de idioma de la app de escritorio se basa en su propia capa de
> i18n (`apps/desktop/src/i18n/`). A diferencia de la versión original empaquetada
> (que solo incluía inglés, chino, japonés y árabe), este fork **registra
> `es` como locale oficial**, por lo que "Español" aparece y funciona.

### Agente (mensajes estáticos)
Algunos mensajes estáticos del agente (aprobaciones de comandos, avisos de
drenaje del gateway) usan `locales/es.yaml`. Para activarlos:

```bash
hermes config set display.language es
```

## Nota importante sobre el alcance de la traducción

Por diseño, Hermes **no traduce la salida conversacional del agente** (lo que
el asistente te escribe, los logs, los errores ni las descripciones de
herramientas). Esa capa queda en inglés. Lo traducido es:

- La **interfaz de la app de escritorio** (menús, botones, ajustes, páginas).
- Los **mensajes estáticos del agente** vía `locales/es.yaml`.

## Cambios aplicados en este fork para habilitar el español en la UI

1. Se copió `web/src/i18n/es.ts` (traducción completa de la UI) a
   `apps/desktop/src/i18n/es.ts`.
2. Se registró el locale en `apps/desktop/src/i18n/catalog.ts` (`TRANSLATIONS`).
3. Se añadió la opción `es` (endónimo "Español") y sus alias
   (`es-es`, `es-mx`, `spanish`, `español`, …) en
   `apps/desktop/src/i18n/languages.ts`.
4. Tras reconstruir el renderer (`npm run build` en `apps/desktop`), el bundle
   de i18n incluye las cadenas en español y el selector de idioma las ofrece.

Para reconstruir desde cero:

```bash
cd apps/desktop
npm install
npm run build          # genera dist/ con español
# luego empaqueta el release:
npm run dist:win
```
