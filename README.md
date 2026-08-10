# Laboratorio 3: SignBridge ASL

Prototipo académico de clasificación de las 29 clases de ASL Alphabet. El proyecto incluye análisis exploratorio, preprocesamiento, comparación de CNN, redes densas y Random Forest, aumento de datos y evaluación con fotografías propias.

Repositorio: [https://github.com/Qu3zada22/Laboratorio3-ds](https://github.com/Qu3zada22/Laboratorio3-ds)

## Resultados principales

- Modelo final: CNN 2 base.
- Validación: `0.986973`.
- Test reservado: pérdida `0.059055`, accuracy `0.986590`.
- Fotografías propias: `2/15` (`0.133333`), con una brecha de dominio de `0.853257`.

El informe final está disponible en [reportes/informe_final_signbridge.pdf](reportes/informe_final_signbridge.pdf).

## Ejecutar con uv y JupyterLab

Requisitos: Python 3.12 o 3.13, [uv](https://docs.astral.sh/uv/) y acceso a Internet para la descarga inicial desde Kaggle mediante KaggleHub.

```bash
uv sync
uv run jupyter lab
```

En JupyterLab, abra `notebooks/01_eda_preprocessing.ipynb` y ejecute las celdas en orden desde un kernel limpio.

Para producir una copia ejecutada limpia sin sobrescribir el notebook versionado:

```bash
uv run jupyter nbconvert --execute --ExecutePreprocessor.timeout=-1 --to notebook --output laboratorio3-executed.ipynb --output-dir /tmp notebooks/01_eda_preprocessing.ipynb
```

El flujo descarga aproximadamente 87,000 imágenes desde Kaggle. El entrenamiento completo es intensivo en CPU y puede tardar decenas de minutos; la ejecución limpia de referencia tomó cerca de 25 minutos. El tiempo depende del equipo.

## Estructura

- `notebooks/01_eda_preprocessing.ipynb`: notebook ejecutado y evidencia principal.
- `reportes/informe_final_signbridge.pdf`: informe final sin listados de código.
- `reportes/informe_final_signbridge.html`: fuente mantenible del informe.
- `reportes/assets/`: figuras extraídas de los outputs almacenados del notebook.
- `pyproject.toml` y `uv.lock`: entorno reproducible administrado por uv.

## Privacidad

Las fotografías originales permanecen fuera de Git mediante las rutas ignoradas `fotos/` y `data/own_photos/`. El PDF y `reportes/assets/10_fotos_propias.png` contienen un montaje derivado de la evaluación; su publicación requiere el consentimiento de las personas participantes.
