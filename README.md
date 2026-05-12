# 📧 MongoDB Email Template — Outlook Optimizado

Plantilla de email HTML lista para producción, optimizada para **Microsoft Outlook Desktop (Word engine)** y **Outlook Web**, con soporte para clientes modernos (Apple Mail, Gmail, Yahoo).

---

## 📁 Archivos

```
mongodb-email-outlook.html   → Plantilla principal lista para producción
README.md                    → Este archivo
```

---

## ✅ Compatibilidad

| Cliente                        | Soporte     |
|-------------------------------|-------------|
| Outlook 2016 / 2019 / 2021    | ✅ Completo |
| Outlook 365 Desktop (Windows) | ✅ Completo |
| Outlook Web (OWA)             | ✅ Completo |
| Apple Mail                    | ✅ Completo |
| Gmail (Web + App)             | ✅ Completo |
| Yahoo Mail                    | ✅ Completo |
| iOS Mail                      | ✅ Completo |
| Android Gmail                 | ✅ Completo |
| Samsung Email                 | ✅ Completo |

---

## 🔧 Hacks de Outlook implementados

| # | Hack | Descripción |
|---|------|-------------|
| 1 | Namespace VML | `xmlns:v` y `xmlns:o` en `<html>` — habilita VML para botones redondeados |
| 2 | Reset Word engine | `mso-table-lspace/rspace: 0pt` — elimina gaps que Word agrega entre celdas |
| 3 | `bgcolor` en atributo HTML | Outlook ignora `background-color` CSS, solo lee el atributo `bgcolor=""` |
| 4 | Wrapper con `align="center"` | `margin: auto` no funciona en Outlook; se usa tabla 100% + `align="center"` |
| 5 | Botones `<v:roundrect>` VML | Única forma de tener `border-radius` real en Outlook Desktop |
| 6 | Ghost tables condicionales | `<!--[if mso]>` para layouts de 2–3 columnas renderizados correctamente |
| 7 | `o:OfficeDocumentSettings` | `<o:AllowPNG/>` evita que Outlook bloquee PNGs con transparencia |
| 8 | Pixel de tracking comentado | Placeholder listo para activar con tu ESP |

---

## 🏷️ Variables de personalización

Estas variables las reemplaza tu **ESP (Email Service Provider)** antes de enviar:

| Variable | Descripción | Ejemplo |
|----------|-------------|---------|
| `{{first_name}}` | Nombre del destinatario | `Jou` |
| `{{email}}` | Email del destinatario | `jou@empresa.com` |

> **Nota:** `{{cta_link}}` ya está reemplazado con la URL real de MongoDB Atlas:  
> `https://www.mongodb.com/cloud/atlas/register`

### Sintaxis por ESP

| ESP | Sintaxis equivalente |
|-----|---------------------|
| Mailchimp | `*\|FNAME\|*` |
| SendGrid | `{{first_name}}` ✅ (nativa) |
| Brevo (Sendinblue) | `{{ contact.FIRSTNAME }}` |
| HubSpot | `{{ contact.firstname }}` |
| Klaviyo | `{{ first_name }}` |

---

## 🔗 UTM Tracking

Todos los enlaces incluyen parámetros UTM para analítica:

```
utm_source=email
utm_medium=campaign
utm_campaign=lanzamiento_producto
utm_content=[sección]
```

### Secciones trackeadas

| `utm_content` | Ubicación |
|---------------|-----------|
| `hero_cta` | Botón principal "Explorar MongoDB 8.0" |
| `code_section_docs` | Link "Ver documentación completa" |
| `resource_university` | Card MongoDB University |
| `resource_webinar` | Card Webinar en Vivo |
| `bottom_cta` | Botón final "Crear mi Atlas Gratuito" |
| `footer_privacy` | Link Privacidad en footer |
| `footer_terms` | Link Términos de Uso en footer |
| `footer_unsubscribe` | Link de baja (requerido CAN-SPAM) |

---

## 🌙 Dark Mode

Implementado con **color-safe design** (sin blancos puros):

- Fondo principal: `#0d1b2a` (no se invierte agresivamente)
- Fondo tarjetas: `#001e2b`
- Verde MongoDB: `#00ed64` (funciona en light y dark)
- Texto principal: `#e8f4f0`
- Texto secundario: `#a8c5ba`
- Override explícito vía `@media (prefers-color-scheme: dark)` para Apple Mail y Outlook iOS

---

## 📱 Diseño Responsive

- Estructura **hybrid design** (fluida sin media queries complejas)
- `max-width: 600px` para desktop
- Columnas se apilan en móvil via `display: inline-block` + clases `.stack-column`
- Botones con mínimo **52px de altura** (zona táctil adecuada)
- Imágenes con `width` adaptable

---

## 🖼️ Logo

El logo usa **SVG inline** para evitar dependencias de servidores externos. Incluye fallback para Outlook Desktop (que no renderiza SVG inline) mediante comentarios condicionales `<!--[if mso]>`.

> ⚠️ No usar imágenes de Wikipedia u otros dominios con hotlink bloqueado.

---

## 🚀 Cómo usar en producción

### 1. Subir a tu ESP
Copia el contenido de `mongodb-email-outlook.html` en el editor HTML de tu plataforma.

### 2. Mapear variables
Configura el merge tag de `{{first_name}}` con el campo "Nombre" de tu lista de contactos.

### 3. Activar pixel de tracking (opcional)
Descomenta la línea al final del `<body>` y reemplaza la URL con la de tu plataforma:
```html
<img src="https://track.tudominio.com/open?campaign=lanzamiento_producto&email={{email}}" 
     width="1" height="1" alt="" style="display:block;border:0;" />
```

### 4. Pruebas recomendadas
- **Litmus** o **Email on Acid** para probar en múltiples clientes
- **Mail Tester** (mail-tester.com) para verificar spam score
- Envío de prueba a cuenta de Outlook.com y Gmail antes de campaña

---

## ⚠️ Restricciones aplicadas

- ❌ No flexbox
- ❌ No CSS Grid
- ❌ No `position: absolute/relative`
- ❌ No `float`
- ❌ No JavaScript (excepto script de preview local, inofensivo)
- ❌ No media queries complejas
- ❌ No fuentes web externas (solo Arial, Helvetica, Georgia, Courier New)
- ✅ CSS 100% inline en elementos críticos
- ✅ Atributos HTML de presentación como fallback (`bgcolor`, `width`, `align`, `valign`)

---

## 📋 Cumplimiento legal

- ✅ **CAN-SPAM**: incluye dirección física y enlace de baja
- ✅ **GDPR**: enlace de baja con email del destinatario
- ✅ **Accesibilidad**: atributos `alt` en todas las imágenes, `role="presentation"` en tablas decorativas

---
Plantilla generada para ejemplo visual.

*Generado para uso con MongoDB 8.0 — *
