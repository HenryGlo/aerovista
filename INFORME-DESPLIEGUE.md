# Informe de Puesta en Producción — AeroVista

**Asignatura:** Estructuras simples para la web
**Universidad Bicentenaria de Aragua — Facultad de Ingeniería de Sistemas**
**Autor:** Henry Gómez · C.I. V-30071779
**Actividad IV:** Animaciones y transiciones web + Ambientes de producción (alojamiento web)

---

## 1. Descripción general

Partiendo del boceto del sitio desarrollado en la actividad anterior, se enriqueció la
*landing page* de la aerolínea ficticia **AeroVista** con lo siguiente:

1. **Nueva sección con animación CSS3** (`#ruta` — *"Sigue nuestra ruta por el cielo"*),
   acorde a la temática aeronáutica del sitio.
2. **Nuevo enlace en el menú de navegación** ("Ruta") integrado con el efecto
   **Smooth Scrolling** de la actividad anterior.
3. **Puesta en producción** del sitio en un hosting gratuito.

> **Nota sobre el hosting:** en lugar de InfinityFree se utilizó **GitHub Pages**, un
> servicio de alojamiento estático **gratuito**. Ofrece HTTPS automático, despliegue
> continuo desde el repositorio y una URL pública permanente, cumpliendo el mismo
> objetivo de la actividad (subir el sitio a un espacio de almacenamiento gratuito y
> ponerlo en funcionamiento).

**URL del sitio en producción:** https://henryglo.github.io/aerovista/
**Repositorio:** https://github.com/HenryGlo/aerovista

---

## 2. La animación CSS3 (solo CSS)

La sección *Ruta* recrea una escena de vuelo construida **100% con CSS3**, sin JavaScript:

| Elemento | Técnica CSS3 empleada |
|----------|-----------------------|
| Cielo | `linear-gradient` (degradado azul de la marca) |
| Sol | `radial-gradient` + `@keyframes brillar` (escala y opacidad pulsante) |
| Nubes | Formas con `border-radius` y pseudo-elementos `::before`/`::after`; movimiento en *parallax* con `@keyframes derivar` y distintas `animation-duration` |
| Avión | Emoji reposicionado con `transform:rotate()` y desplazado con `@keyframes volar` (`translateX`/`translateY`) |
| Estela (contrail) | Pseudo-elemento `::after` con `linear-gradient` que se desvanece |
| Accesibilidad | `@media (prefers-reduced-motion:reduce)` desactiva las animaciones |

El enlace del menú `#ruta` aprovecha el Smooth Scrolling ya definido en la hoja de
estilos mediante `html{ scroll-behavior:smooth }`, por lo que al hacer clic el navegador
se desliza suavemente hasta la nueva sección.

---

## 3. Puesta en producción — paso a paso

### Paso 1 — Preparar el repositorio local (Git)

```bash
git init
git config user.name  "Henry Gomez"
git config user.email "henrylofiego@gmail.com"
git branch -M main
git add .
git commit -m "Actividad IV - Configuracion inicial del repositorio del proyecto AeroVista"
```

Se registraron *commits* con nomenclatura académica que documentan el avance:

```
Actividad IV - Nueva seccion 'Ruta de vuelo' con animacion CSS3 e integracion de SmoothScrolling en el menu
Actividad III - Boceto base del sitio: paginas internas, recursos multimedia y hoja de estilos
Actividad IV - Configuracion inicial del repositorio del proyecto AeroVista
```

> **Captura 1:** Historial de commits del repositorio.

### Paso 2 — Crear la cuenta / repositorio en el hosting gratuito

Se utilizó la cuenta gratuita de **GitHub** (usuario `HenryGlo`) y se creó un repositorio
**público** llamado `aerovista`:

```bash
gh repo create aerovista --public --source=. --remote=origin --push
```

> **Captura 2:** Página del repositorio `HenryGlo/aerovista` en GitHub mostrando los
> archivos del sitio y el *deployment* `github-pages` activo.

### Paso 3 — Subir el sitio al espacio de almacenamiento

El comando anterior subió (`push`) todos los archivos del sitio (`index.html`,
`destinos.html`, `flota.html`, `experiencia.html`, `tematica.html`, carpetas `img/` y
`video/`) a la rama `main` del repositorio remoto.

### Paso 4 — Activar y poner en funcionamiento GitHub Pages

Se habilitó GitHub Pages sobre la rama `main`, carpeta raíz (`/`):

```bash
gh api -X POST repos/HenryGlo/aerovista/pages \
  -f "source[branch]=main" -f "source[path]=/"
```

*(Equivale, en la interfaz web, a: **Settings → Pages → Source: Deploy from a branch →
Branch: `main` / `root` → Save**.)*

El servicio construyó el sitio (`status: building` → `status: built`) y quedó publicado.
Se verificó que responde correctamente:

```bash
curl -s -o /dev/null -w "%{http_code}" https://henryglo.github.io/aerovista/
# 200
```

> **Captura 3:** Ajustes de GitHub Pages con el mensaje *"Your site is live at
> https://henryglo.github.io/aerovista/"*.

### Paso 5 — Verificación del sitio en producción

Se abrió la URL pública y se comprobó que:

- El sitio carga correctamente por **HTTPS**.
- El menú muestra el nuevo enlace **"Ruta"**.
- Al hacer clic en "Ruta", el **Smooth Scrolling** desliza suavemente hasta la sección.
- La **animación CSS3** se reproduce: el sol brilla, las nubes derivan y el avión cruza
  el cielo con su estela.

> **Captura 4:** Sección *"Ruta"* en producción con la animación funcionando.

---

## 4. Conclusión

El sitio de AeroVista quedó **en funcionamiento en producción** sobre un hosting gratuito
(GitHub Pages), enriquecido con una nueva sección animada con **CSS3** e integrada al menú
mediante **Smooth Scrolling**, cumpliendo todos los objetivos de la actividad.

**Sitio en vivo:** https://henryglo.github.io/aerovista/
