# Champions Hub — cómo dejarlo funcionando

Esta carpeta tiene todo lo necesario:

```
champions-hub/
├── index.html          ← página pública, solo lectura, la ve cualquiera
├── admin.html           ← panel privado de edición (no lo enlaces en redes)
├── style.css             ← estilos compartidos
└── data/
    ├── torneos.json
    ├── tiers.json
    ├── equipos.json
    ├── pokedex_builds.json
    ├── pokedex_species.json
    ├── liga_config.json
    ├── liga_calendario.json
    ├── liga_jugadores.json
    └── liga_playoffs.json   ← se crea solo al guardar el primer resultado de playoffs
```

## Tabla de posiciones y Playoffs

La **tabla general de posiciones** se calcula sola con los resultados que capturas en Liga (fecha por fecha) — no hay nada que llenar aparte. Se ordena por partidos ganados y, en caso de empate, por porcentaje de victorias.

Los **playoffs** (Top 4) se desbloquean automáticamente al terminar las fechas de la fase regular, con el emparejamiento clásico #1 vs #4 y #2 vs #3. Desde `admin.html → Playoffs` solo indicas quién ganó cada llave (semifinales, final y tercer puesto); el sitio público arma el bracket solo.

`index.html` **solo lee** estos JSON. `admin.html` es la única forma de escribirlos, y solo funciona si tienes un token de GitHub con permiso de escritura sobre tu repositorio — así que aunque alguien encuentre la URL de `admin.html`, sin tu token no puede guardar nada.

## 1. Crea el repositorio en GitHub

1. Entra a github.com → **New repository**.
2. Ponle un nombre, por ejemplo `champions-hub`. Puede ser público (para que GitHub Pages sea gratis) o privado si prefieres.
3. Sube todos los archivos de esta carpeta manteniendo la estructura (incluida la carpeta `data/`).

## 2. Activa GitHub Pages

1. En el repo: **Settings → Pages**.
2. En "Source" elige la rama `main` y la carpeta `/ (root)`.
3. Guarda. En un par de minutos tu página pública quedará en algo como:
   `https://TU-USUARIO.github.io/champions-hub/`

Esa es la URL que compartes con la comunidad — es de **solo lectura**.

## 3. Crea tu token de GitHub (para editar)

1. GitHub → foto de perfil → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. **Repository access:** elige "Only select repositories" y selecciona tu repo `champions-hub` (nunca des acceso a todos tus repos).
3. **Permissions → Repository permissions → Contents:** ponlo en **Read and write**.
4. Genera el token y **cópialo ya** — GitHub solo lo muestra una vez.
5. Guárdalo en un gestor de contraseñas. No lo compartas, no lo subas a ningún archivo del repo.

## 4. Entra al panel de administración

1. Abre `https://TU-USUARIO.github.io/champions-hub/admin.html` (o el archivo local en tu computadora).
2. Completa: **Usuario**, **Repositorio**, **Rama** (`main`) y pega tu **Token**.
3. "Conectar y cargar datos". Desde ahí editas Torneos, Tier List, Equipos, Pokédex y el roster de especies.
4. Cada vez que guardas algo, se hace un **commit real** a tu repositorio — puedes ver el historial completo en la pestaña "Commits" de GitHub, y revertir cualquier cambio si algo sale mal. Nada se borra de verdad: siempre queda en el historial de Git.
5. La página pública puede tardar uno o dos minutos en reflejar el cambio (tiempo normal de build de GitHub Pages + caché del navegador).

## Notas de seguridad

- El token vive **solo en el navegador donde lo escribiste** (localStorage). Si usas otra computadora, tienes que volver a pegarlo ahí.
- Si crees que el token se filtró, bórralo desde GitHub (Settings → Developer settings → tokens → Delete) y crea uno nuevo.
- No es necesario ni recomendable ocultar `admin.html` con contraseñas adicionales: la seguridad real la da el token, no la URL.
- Si en el futuro quieres que otra persona de confianza edite también, dale su propio token de acceso al repo (o hazla colaboradora) — no compartas el tuyo.
