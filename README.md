# ML + Android — Clasificación de objetos en tiempo real

Demo de Machine Learning **on-device** en Android: usa la cámara en vivo (CameraX)
y un modelo pre-entrenado de ML Kit (Image Labeling) para identificar objetos y
escenas en tiempo real, sin conexión a internet y con inferencia local.

## Requisitos mínimos de ejecución

- Android Studio Koala o superior
- `minSdk 24` (Android 7.0+)
- Un dispositivo físico con cámara trasera

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