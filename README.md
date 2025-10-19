# Aplicación Ionic - Icono Personalizado y Splash Screen

## Descripción

Aplicación móvil desarrollada con **Ionic Framework** y **Angular** que implementa funcionalidades de cámara, icono personalizado y splash screen personalizado.

**Autor:** Edwin Sarango  
**Curso:** Aplicaciones Móviles  
**Tarea:** Tarea 2 - Implementación de Icono y Splash Screen Personalizados

---

##  Características Principales

### 1. Funcionalidad de Cámara
- Integración con **Capacitor Camera API**
- Captura de fotos desde la cámara del dispositivo
- Visualización de la foto capturada en tiempo real
- Interfaz intuitiva con botón flotante (FAB)

### 2. Icono Personalizado
- Icono personalizado de la aplicación
- Configurado para Android.
- Múltiples resoluciones para diferentes dispositivos

### 3. Splash Screen Personalizado
- Splash screen personalizado con duración de **3 segundos**
- Configuración automática con `@capacitor/splash-screen`
- Transición suave al iniciar la aplicación

### 4. Interfaz Moderna
- Diseño responsivo con **Ionic Components**
- Sistema de tabs para navegación
- Iconos personalizados en la barra de navegación
- Estilos CSS personalizados

---

## Tecnologías Utilizadas

- **Ionic Framework** v8.0.0
- **Angular** v20.0.0
- **Capacitor** v7.4.3
- **TypeScript** v5.8.0
- **Node.js** y **npm**

### Plugins de Capacitor

```json
{
  "@capacitor/camera": "^7.0.2",
  "@capacitor/splash-screen": "^7.0.3",
}
```

---

## Instalación

### Prerrequisitos

- Node.js (v16 o superior)
- npm o yarn
- Ionic CLI
- Android Studio (para desarrollo Android)
- Xcode (para desarrollo iOS, solo en macOS)


## Uso de la Funcionalidad de Cámara

### Código de Implementación

**tab1.page.ts**
```typescript
import { Camera, CameraResultType, CameraSource } from '@capacitor/camera';

async takePicture() {
  try {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.Uri,
      source: CameraSource.Camera
    });

    this.photo = image.webPath;
  } catch (error) {
    console.error('Error al tomar la foto:', error);
  }
}
```

### Permisos Necesarios

La aplicación solicitará automáticamente los siguientes permisos:
- **Android:** `CAMERA`, `READ_EXTERNAL_STORAGE`, `WRITE_EXTERNAL_STORAGE`
- **iOS:** `NSCameraUsageDescription`, `NSPhotoLibraryUsageDescription`

---

## Configuración del Icono Personalizado

### Ubicación de los Recursos

Los iconos personalizados se encuentran en:
```
resources/
  ├── icon.png (1024x1024px)
  └── splash.png (2732x2732px)
```

### Generar Iconos para Todas las Plataformas

```bash
npx capacitor-assets generate
```

Este comando genera automáticamente:
- Iconos para Android (todas las densidades)
- Splash screens adaptados a cada plataforma

---

## Configuración del Splash Screen

### Código de Implementación

**app.component.ts**
```typescript
import { SplashScreen } from '@capacitor/splash-screen';

async showsplash() {
  await SplashScreen.show({
    autoHide: true,
    showDuration: 3000,
  });
}
```

### Características
- **Duración:** 3 segundos
- **Auto-hide:** Se oculta automáticamente
- **Personalizable:** Imagen y colores configurables

---

## 📁 Estructura del Proyecto

```
iconopersonalizado/
├── android/                    # Proyecto Android nativo
├── ios/                        # Proyecto iOS nativo
├── src/
│   ├── app/
│   │   ├── tab1/              # Tab con funcionalidad de cámara
│   │   │   ├── tab1.page.ts
│   │   │   ├── tab1.page.html
│   │   │   └── tab1.page.scss
│   │   ├── tabs/              # Sistema de navegación por tabs
│   │   └── app.component.ts   # Componente principal con splash
│   ├── assets/                # Recursos estáticos
│   └── theme/                 # Estilos globales
├── resources/                 # Iconos y splash screens
├── capacitor.config.ts        # Configuración de Capacitor
├── package.json
└── README.md
```

---

## Funcionalidades por Tab

### Tab 1 - Cámara 📷
- Captura de fotos con la cámara del dispositivo
- Visualización de la foto capturada
- Botón flotante para acceso rápido
- Texto explicativo de la aplicación

### Tab 2
- Contenido de ejemplo

### Tab 3
- Contenido de ejemplo

---

## Configuración Adicional

### capacitor.config.ts

```typescript
import type { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'io.ionic.starter',
  appName: 'iconopersonalizado',
  webDir: 'www',
  plugins: {
    SplashScreen: {
      launchShowDuration: 3000,
      launchAutoHide: true,
      backgroundColor: "#ffffffff",
      androidSplashResourceName: "splash",
      androidScaleType: "CENTER_CROP",
      showSpinner: false,
      androidSpinnerStyle: "large",
      iosSpinnerStyle: "small",
      spinnerColor: "#999999",
      splashFullScreen: false,
      splashImmersive: false,
    }
  }
};

export default config;
```

---

## Compilación para Producción

### Android

1. **Generar APK de depuración**
```bash
ionic build
npx cap sync android
npx cap open android
```

2. **En Android Studio:**
   - Build > Build Bundle(s) / APK(s) > Build APK(s)

3. **Generar APK firmado (Release)**
   - Build > Generate Signed Bundle / APK
   - Seguir el asistente de firma

## Recursos Adicionales

- [Documentación de Ionic](https://ionicframework.com/docs)
- [Capacitor Camera API](https://capacitorjs.com/docs/apis/camera)
- [Capacitor Splash Screen](https://capacitorjs.com/docs/apis/splash-screen)
- [Angular Documentation](https://angular.io/docs)

---

## Licencia

Este proyecto fue desarrollado con fines educativos para el curso de Aplicaciones Móviles.

---
