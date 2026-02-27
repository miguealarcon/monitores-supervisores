# 🎯 Sistema de Registro y Monitoreo VANCAN 2026

Sistema web completo para registro de actividades y monitoreo de la **Vacunación Activa para Niños en Arequipa (VANCAN)** 2026.

Acceso único: **[https://TU_USUARIO.github.io/monitores/](https://miguealarcon.github.io/monitores-supervisores/)**

## 📋 Descripción

Sistema compuesto por **dos formularios independientes** que se guardan automáticamente en Google Sheets:

### Formulario 1: Monitoreo
Registro general de participación y supervisión de actividades VANCAN (participantes de microred, estado de materiales, supervisión).

### Formulario 2: Monitoreo-2
Registro específico de vacunación (equipos, movilidad, incidentes detectados).

## 🌐 Acceso

Una vez desplegado en GitHub Pages, acceder con cualquier navegador a:
```
https://TU_USUARIO.github.io/monitores/
```

Seleccionar el formulario deseado y comenzar a registrar datos.

## 🗂️ Estructura del Proyecto

```
monitores/
├── index.html                 # Página de inicio (portada)
├── monitoreo.html             # Formulario 1
├── monitoreo-2.html           # Formulario 2
├── codigo.gs                  # Backend (Google Apps Script)
├── VARIABLES.md               # Documentación de variables
└── README.md                  # Este archivo
```

## 🛠️ Stack Tecnológico

### Frontend
- HTML5, CSS3, Vanilla JavaScript
- Validación de formularios en cliente
- Interfaz responsive (mobile + desktop)

### Backend
- Google Apps Script
- Autenticación por usuario/contraseña
- Ruteo inteligente de datos por formulario

### Hosting
- GitHub Pages (despliegue automático desde repositorio)
- Acceso gratuito sin servidores adicionales

### Database
- Google Sheets
- Dos hojas independientes (Resultados_Monitoreo, Resultados_Monitoreo2)
- Encabezados auto-generados en primer envío

### API
- Comunicación formulario → Google Apps Script via fetch()
- Respuestas JSON para validación instantánea

## 📖 Formularios Detalle

### Formulario 1: Monitoreo

**Secciones:**
1. **I. APERTURA**: Participantes de microred y estado de materiales
2. **II. DESARROLLO**: Supervisión (gerencia, red, microred, etc.)
3. **CIERRE**: Observaciones finales

**Campos principales:**
- Microred
- Fecha
- Participantes (MR, Adicionales)
- Estado de materiales (termos, EPP)
- Supervisión
- Cadena de frío
- Promoción de la salud
- Observaciones

### Formulario 2: Monitoreo-2

**Secciones:**
1. **I. APERTURA**: Movilidad (buses, camionetas, autos)
2. **II. VACUNACIÓN**: Equipos planeados, en campo, perifoneo
3. **III. CIERRE**: Incidentes (6 tipos), observaciones

**Campos principales:**
- Microred
- Fecha
- Usuario
- Movilidad (JSON)
- Equipos (planeados vs campo)
- Perifoneo
- Incidentes:
  - Ninguno (bloquea otras opciones)
  - Mordeduras
  - Reacciones alérgicas
  - Falta de materiales
  - Falta de vacunas
  - Problemas con pobladores
  - Otros

## ⚙️ Instalación y Configuración

### Paso 1: Preparar Google Apps Script

1. Ve a [script.google.com](https://script.google.com)
2. Crea un nuevo proyecto
3. Copia el contenido de `codigo.gs` desde este repositorio
4. En la función `doPost()`, reemplaza `const ss = SpreadsheetApp.openById("aqui_va_tu_id");` con el ID de tu hoja de cálculo
5. Guarda el proyecto

### Paso 2: Desplegar Web App

1. En Google Apps Script → **Deploy** → **New deployment**
2. Tipo: **Web app**
3. Execute as: Tu cuenta
4. Who has access: **Anyone**
5. Copia la URL mostrada (ejemplo: `https://script.google.com/macros/s/ABC123XYZ/exec`)

### Paso 3: Actualizar Formularios

En `monitoreo.html` y `monitoreo-2.html` (línea ~50), busca:
```js
const url = "https://script.google.com/macros/s/AQUI_VA_TU_ID/exec";
```

Reemplázala con tu URL del paso anterior.

### Paso 4: Crear Google Sheet

1. Crea una nueva hoja de cálculo en Google Drive
2. Los encabezados se crearán automáticamente en el primer envío
3. Copia el ID de la hoja (en la URL: `docs.google.com/spreadsheets/d/` + ID)
4. Asegúrate de que es compartida con tu cuenta de Google Apps Script

### Paso 5: Subir a GitHub Pages

```bash
# Clonar este repositorio o crear uno nuevo
mkdir monitores && cd monitores

# Copiar archivos
cp -r /home/cayetano/Escritorio/monitores/* .

# Inicializar Git
git init
git add .
git commit -m "Sistema VANCAN 2026"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/monitores.git
git push -u origin main
```

### Paso 6: Habilitar GitHub Pages

1. Ve a tu repositorio en GitHub
2. **Settings** → **Pages**
3. Source: **main** (rama)
4. Guardar

**Tu sitio estará disponible en:** `https://TU_USUARIO.github.io/monitores/`

## 📊 Base de Datos

### Hojas Automáticas

Los datos se distribuyen en dos hojas dentro de la misma hoja de cálculo:

- **Resultados_Monitoreo**: Datos del formulario Monitoreo
- **Resultados_Monitoreo2**: Datos del formulario Monitoreo-2

### Auto-Creación de Encabezados

La función `asegurarEncabezados()` se ejecuta en cada envío:
- Si la hoja está vacía → crea todos los encabezados automáticamente
- Si la hoja tiene datos → identifica columnas faltantes y las agrega al final

No requiere configuración manual de columnas.

## 📝 Variables y Documentación

Para la lista completa de variables por formulario, revisa [VARIABLES.md](VARIABLES.md)

Incluye:
- Nombres exactos de campos (ID HTML)
- Tipo de dato
- Valores posibles
- Dependencias (campos condicionales)

## 🔍 Depuración

### Ver datos en Console del navegador

1. Abre el formulario en tu navegador
2. Presiona **F12** para abrir DevTools
3. Selecciona pestaña **Console**
4. Completa el formulario y haz submit
5. Verás el log:
```
=== datos formulario Monitoreo2 ===
microred : ASA
fecha : 2026-02-26
equipos_planeados : 5
equipos_campo : 4
perifoneo : Si
perifoneo_cant : 150
inc_mordeduras-check : on
inc_mordeduras-cant : 2
...
```

### Logs en Google Apps Script

1. Ve a [script.google.com](https://script.google.com)
2. Abre tu proyecto
3. **Ejecuciones** (lado izquierdo)
4. Selecciona una ejecución para ver logs y errores

### Mensaje de usuario

Cada formulario muestra confirmación visual:
- ✅ "Datos guardados correctamente" → envío exitoso
- ❌ "Error: [mensaje]" → problema (revisa URL de Google Apps Script)

## ✅ Checklist de Deploy

- [ ] Google Apps Script creado y desplegado como Web App
- [ ] URLs de Web App actualizado en ambos formularios
- [ ] Google Sheet creada y compartida
- [ ] Repositorio GitHub creado
- [ ] Archivos HTML (index.html, monitoreo.html, monitoreo-2.html) en raíz
- [ ] GitHub Pages habilitado (Settings → Pages)
- [ ] Proyecto con rama main empujada a GitHub
- [ ] Test: Acceder a `https://TU_USUARIO.github.io/monitores/`
- [ ] Test: Llenar y enviar formulario
- [ ] Test: Verificar console.log (F12)
- [ ] Test: Verificar datos en Google Sheets

## 🖥️ Requisitos

- Navegador moderno (Chrome, Firefox, Safari, Edge)
- Cuenta de Google
- Acceso a Google Sheets
- Conexión a Internet
- No requiere instalación local

## 🎨 Características

✅ Formularios responsivos (mobile + desktop)
✅ Campos condicionales (aparecen/desaparecen según respuestas)
✅ Validación de números automática (min=0)
✅ "Ninguno" bloquea otras opciones automáticamente
✅ Autenticación por usuario/contraseña
✅ Guardado automático en Google Sheets
✅ Encabezados auto-generados
✅ Console logging para debugging
✅ Interfaz intuitiva con iconos

## 📋 Campos Condicionales

Algunos campos solo aparecen si se selecciona una opción específica:

### Monitoreo-2
- **perifoneo_cant** (cantidad): Solo si `perifoneo` = "Si"
- **otros** (Otros retrasos): Solo si se marca "Otros" en retrasos
- **Incidentes detallados**: Solo si no se marca "Ninguno"
  - inc_mordeduras-cant, inc_mordeduras-esp
  - inc_alergicas-cant, inc_alergicas-esp
  - ...etc

### Monitoreo
- Campos "¿Quién?" en supervisión: Solo si se marca opción correspondiente

## 🚀 Mejoras Futuras

- [ ] Gráficos en tiempo real en portal de admin
- [ ] Exportación a PDF
- [ ] Sincronización offline (localStorage)
- [ ] Roles y permisos por usuario
- [ ] Análisis de datos por período

## 📞 Soporte

En caso de problemas:

1. **Formulario no envía datos**
   - Abre Console (F12)
   - Verifica que URL de Google Apps Script es válida
   - Revisa permisos de la Google Sheet

2. **Campos condicionales no funcionan**
   - Recarga la página (F5)
   - Verifica que JavaScript está habilitado
   - Abre Console (F12) para ver errores

3. **Login no funciona**
   - Verifica usuario/contraseña
   - Revisa que Google Apps Script está deployado como "Anyone"

---

## 📄 Licencia

Proyecto interno VANCAN 2026 - Arequipa

**Versión**: 2.1  
**Última actualización**: 26 de febrero de 2026  
**Estado**: ✅ Producción (GitHub Pages)
