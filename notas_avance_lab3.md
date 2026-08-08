# Laboratorio 3 — Notas de avance (ejercicios 1-6 completos)

## Resultados de los modelos (ejercicios 4-6)

| Modelo | Accuracy en test |
|---|---|
| **CNN 2** (mejor) | 0.982 |
| Random Forest (n_estimators=300) | 0.967 |
| CNN 1 | 0.916 |
| Red simple (fully-connected) | 0.760 |

**Mejor modelo: `cnn_2`**, guardado en esa variable dentro del notebook. Es el que se debe usar en los ejercicios 7 y 8.

## Qué falta (ejercicios 7 al 10)

### Ejercicio 7 — Image augmentation
- Reentrenar los modelos (al menos `cnn_2`, idealmente también `cnn_1`) con transformaciones de augmentation.
- Responder explícitamente en el notebook: ¿por qué un flip horizontal cambia el significado de una seña en vez de solo aumentar los datos? (una mano derecha se convierte en la seña de otra letra, no en la misma letra vista distinto — a diferencia de gatos/perros, donde el sujeto sigue siendo el mismo).
- Definir qué transformaciones sí tienen sentido para señas (rotación leve, zoom, cambios de brillo/contraste) y cuáles no (flip horizontal, flip vertical) y por qué.

### Ejercicio 8 — Prueba con fotos propias
- Usar `cnn_2` (el mejor modelo).
- Mínimo 5 letras distintas por integrante del grupo, fotografiadas por ustedes mismos.
- Documentar accuracy/resultados y discutir por qué falla o acierta (condiciones de luz, fondo, ángulo distintos al dataset).

### Ejercicio 9 — Accesibilidad y sesgo
- Reflexionar sobre limitaciones del dataset: tono de piel, ángulo de cámara, iluminación, tamaño de mano.
- Dar **al menos una recomendación concreta** (no genérica) para acercar el prototipo a un caso de uso real de SignBridge.

### Ejercicio 10 — Informe final
- No hace falta PDF aparte: la interpretación y conclusiones van en celdas markdown dentro del mismo notebook.
- Debe quedar: EDA + descripción de modelos + efectividad de cada uno + comparación + reflexión de accesibilidad, todo consolidado.

## Cosas importantes para quien continúe

**Variables ya disponibles en el notebook** (no hay que recrearlas):
- `cnn_1`, `cnn_2`, `nn_simple`, `rf_final` — los 4 modelos ya entrenados.
- `best_cnn` — apunta a `cnn_2`.
- `encoder` — `LabelEncoder` ajustado con las clases (`encoder.classes_` da el orden de las 29 clases).
- `X_train`, `y_train`, `X_val`, `y_val`, `X_test`, `y_test` — arreglos ya preprocesados (64x64, normalizados, one-hot).
- `load_and_preprocess(filepath)` — función para cargar y preprocesar una imagen nueva (útil para el ejercicio 8, con las fotos propias).
- `CLASSES` — lista de las 29 clases en orden alfabético/carpeta.

**Decisiones ya tomadas y documentadas** (no hace falta volver a justificarlas, solo mencionarlas si se referencian):
- Submuestra: 600 imágenes por clase, dividida en el split 70/15/15 ya definido sobre el dataset completo.
- Resolución: resize de 200x200 a 64x64.
- Normalización: valores de píxel a [0, 1].

**Detalles técnicos a tener en cuenta:**
- El dataset se descarga con `kagglehub.dataset_download("grassknoted/asl-alphabet")`, no desde una ruta manual.
- Requiere Python 3.12 o 3.13 en el `.venv` (TensorFlow no tiene wheels para 3.14 todavía).
- Si el kernel se reinicia, hay que correr **todo el notebook desde el inicio en orden** — varias celdas dependen de imports y variables definidas en celdas anteriores (por ejemplo `to_categorical`, `encoder`, `X_train`).

**Limitación a mencionar en la discusión final (ejercicio 9 o en la comparación):**
El accuracy tan alto de CNN 2 (0.982) podría estar algo inflado por una característica conocida del dataset ASL Alphabet de Kaggle: muchas imágenes de una misma clase vienen de fotogramas muy similares (casi el mismo frame de un video), y es posible que fotos casi idénticas hayan quedado repartidas entre train/val/test pese al split estratificado. Vale la pena mencionarlo como limitación, especialmente al contrastar el buen desempeño en el dataset contra el desempeño esperado con las fotos propias del ejercicio 8, que van a tener condiciones mucho más variadas.
