# LINK Control

Repositorio del código y publicaciones de **LINK Control** (antes AppControl), compañero Android de [NOVORA-LINK](https://github.com/aroonvaldes-star/NOVORA-LINK).

- **Última APK publicada:** **1.4.128 / código 128** ([`v1.4.128`](https://github.com/aroonvaldes-star/LINK-CONTROL/releases/tag/v1.4.128)), paquete `com.linkcontrol.novora`, Android 11 / API 30 o posterior, Release ARM64.
- **Estado de fuente en este repositorio:** mantiene el snapshot sincronizado del 19 de octubre de 2026 (`1.4.113 / código 113` en `src/NOVORA.Android/NLProjectAndroid.csproj`); el desarrollo canónico activo continúa en `NOVORA-LINK` (`Dev_Local/src/ANDROID`).

## Código y compilación

En este repositorio, el proyecto está en `src/NOVORA.Android/NLProjectAndroid.csproj`. `src/NOVORA` contiene únicamente contratos, utilidades y recursos enlazados necesarios para Android y sus pruebas; no es una copia del escritorio completo.

Requiere .NET 10 y la carga de trabajo Android. Verificar el código sin generar una nueva APK:

```powershell
dotnet workload restore src/NOVORA.Android/NLProjectAndroid.csproj
dotnet build src/NOVORA.Android/NLProjectAndroid.csproj -c Release -r android-arm64 -t:Compile -p:AndroidBuildApplicationPackage=false
./scripts/Test-NOVORA-CI.ps1 -Configuration Release
```

CI compila y ejecuta pruebas de contrato; no instala, firma ni publica APK, ni valida sesiones físicas USB/LAN. No se versionan `bin/`, `obj/` ni claves de firma.

## Publicaciones y política de distribución

Cada release oficial se publica bajo el tag `v<versionName>` con los tres artefactos verificables: `LinkControl.apk` firmada, `NLAndroidRelease.json` y `SHA256SUMS.txt`.

- **Clave de firma vigente (desde `1.4.125`):** `CN=LINK Control, O=NOVORA, C=MX` (huella SHA-256 `8294e639…ca5e030`). Si tienes instalada la `1.4.124` o anterior, desinstálala una sola vez antes de instalar `1.4.125` o superior.
- **Actualizador integrado en Android:** desde `v1.4.125`, LINK Control consulta este repositorio (`releases/latest`), descarga `LinkControl.apk`, valida tamaño, etiqueta, `NLAndroidRelease.json` y SHA-256, e instala la actualización cuando la firma coincide.
- **Historial reciente:**
  - **`v1.4.128`** (Latest): detección física de cable USB frente a **ADB Wi-Fi** (`NLAndroidRouteLabel`) en tarjeta de ruta, botón de transporte, notificación, Configuración, Compartir y LinkEngine; incluye los cambios acumulados de las compilaciones internas `1.4.126` y `1.4.127` (botón «Elegir USB o Wi-Fi» y acceso directo a «Enlazar con código»), las cuales fueron probadas localmente y sustituidas por `1.4.128` sin APK independiente archivada.
  - **`v1.4.125`**: conexión dinámica USB → Wi-Fi, perfiles de datos móviles (VBR desde 100 kbit/s · 1 fps), actualizador integrado desde este repositorio y migración a la clave de firma actual.
  - **`v1.4.111` – `v1.4.124`**: releases históricas conservadas con la firma anterior (`1.4.110` continúa pendiente de localizar).

Toda APK nueva requiere versión `N+1`, firma compatible y comprobación de manifiesto, hash y certificado. Nunca publicar keystores, contraseñas ni tokens.
