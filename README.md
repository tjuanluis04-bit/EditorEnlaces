# Organizador de Enlaces

App Android (WebView) con tres herramientas para transformar listas de enlaces:

1. **Ytdlleech** — genera comandos `/ytdlleech` numerados por página, con título y usuario extraídos de la URL.
2. **Bloques Telegram** — agrupa enlaces `t.me/c/...` consecutivos en bloques de máximo 30 números.
3. **Lista con check** — numera cada enlace y le agrega la marca `[ ✅ ]`.

Toda la lógica corre localmente en el teléfono (HTML/JS embebido), sin necesidad de internet.

## Cómo compilar el APK con GitHub Actions

1. Sube esta carpeta completa a un repositorio de GitHub (rama `main`).
2. Ve a la pestaña **Actions** del repositorio.
3. El workflow **Build APK** se ejecuta automáticamente en cada `push`, o puedes lanzarlo manualmente con **Run workflow**.
4. Al terminar, entra al resumen de la ejecución y descarga el artefacto `app-debug` (o `app-release-unsigned`) desde la sección **Artifacts**.
5. Instala el archivo `.apk` en tu teléfono Android (activa "Instalar apps desconocidas" si es necesario).

## Estructura del proyecto

```
EnlacesApp/
├── .github/workflows/build.yml     ← workflow de compilación
├── app/
│   ├── build.gradle
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/.../MainActivity.kt
│       ├── res/                    ← ícono adaptativo, colores, tema
│       └── assets/index.html       ← interfaz y lógica de las 3 herramientas
├── build.gradle
└── settings.gradle
```

## Personalizar el ícono

El ícono adaptativo está definido en:
- `app/src/main/res/drawable/ic_launcher_background.xml`
- `app/src/main/res/drawable/ic_launcher_foreground.xml`

Puedes reemplazar estos vectores por tu propio diseño; Android generará automáticamente todas las variantes (redondo, cuadrado, "squircle", etc.) en tiempo de compilación.

## Notas

- `minSdk` está fijado en 26 (Android 8.0) porque los íconos adaptativos requieren esa versión como mínimo.
- El APK generado por el workflow **no está firmado** para distribución en Play Store; solo sirve para instalación directa/pruebas. Si necesitas publicarlo, deberás firmar el APK/AAB con tu propia clave.
