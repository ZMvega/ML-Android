# ML Kit Demo — Clasificación de objetos en tiempo real

Demo de Machine Learning **on-device** en Android: usa la cámara en vivo (CameraX)
y un modelo pre-entrenado de ML Kit (Image Labeling) para identificar objetos y
escenas en tiempo real, sin conexión a internet y con inferencia local.

## Cómo abrir el proyecto

1. Abre Android Studio.
2. `File > Open...` y selecciona la carpeta `MLKitDemo` (la raíz, donde está `settings.gradle`).
3. Deja que Gradle sincronice (puede tardar la primera vez mientras descarga CameraX y ML Kit).
4. Conecta un celular Android físico por USB con depuración activada (la cámara no funciona bien en el emulador para este caso) o usa un emulador con soporte de cámara virtual.
5. Dale Run ▶ sobre el módulo `app`.
6. Acepta el permiso de cámara cuando la app lo solicite.
7. Apunta el celular a distintos objetos del salón: la etiqueta inferior cambiará en tiempo real mostrando la clase detectada y el porcentaje de confianza.

## Requisitos mínimos

- Android Studio Koala o superior
- `minSdk 24` (Android 7.0+)
- Un dispositivo físico con cámara trasera (recomendado para la demo en vivo)

## Qué demuestra esta app, en relación con la exposición

- **Inferencia on-device:** todo el procesamiento de la imagen ocurre dentro del
  método `analyzeImage()` en `MainActivity.kt`, usando el cliente `ImageLabeling`
  de ML Kit — no hay ninguna llamada de red.
- **Baja latencia:** el resultado se actualiza prácticamente al instante, frame
  a frame, gracias a `ImageAnalysis.STRATEGY_KEEP_ONLY_LATEST`.
- **Sin necesidad de entrenar ni convertir un modelo:** ML Kit ya trae un modelo
  base capaz de reconocer cientos de objetos y escenas comunes, lo que hace
  que este ejemplo sea seguro de preparar y ejecutar en vivo durante la
  exposición.

## Posible extensión (si se quiere ir más allá)

Reemplazar `ImageLabeling.getClient(ImageLabelerOptions.DEFAULT_OPTIONS)` por
un `LocalModel` propio entrenado en Google Colab (transfer learning sobre
MobileNet) y exportado a `.tflite`, usando
`CustomImageLabelerOptions.Builder(localModel)` en lugar de las opciones por
defecto. Esto permite mostrar el flujo completo: entrenamiento → exportación →
integración, tal como se explicó en la sección de arquitectura de la
exposición.
