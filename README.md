# Laboratorio 12 - Power BI

Repositorio del avance del Laboratorio 12 de Data Science.

https://github.com/UVG-Tareas-y-proyectos/LAB12_DS

## Archivos de entrega

- `Observatorio.pbix`: informe de Power BI con los datos cargados.
- `powerbi/Observatorio.pbip`: proyecto editable y versionable de Power BI.
- `avance_lab12.pdf`: informe de avance.
- `avance_lab12.docx`: versión editable del informe.

## Abrir el informe

1. Abra `Observatorio.pbix` con Power BI Desktop para Windows.
2. Para actualizar los datos, entre a **Transformar datos → Administrar parámetros**.
3. Cambie `RutaDatos` por la ruta absoluta de `data/processed` dentro de esta copia del repositorio.
4. Aplique los cambios y pulse **Actualizar**.

El informe incluye las páginas **Exploración** y **Modelos y estacionalidad**. En Exploración, seleccionar un mes de la serie actualiza los indicadores y el desglose por vía. En la segunda página se comparan MAE y RMSE y se muestra la serie observada frente a la estimación LSTM.

## Estructura

```text
Observatorio.pbix       archivo de Power BI
avance_lab12.pdf        informe entregable
avance_lab12.docx       informe editable
data/raw/               fuentes originales
data/processed/         archivos utilizados por Power BI
powerbi/                proyecto PBIP versionable
docs/evidencias/        evidencias del avance
docs/*.csv              formatos de comparación y registro
referencia/lab10/       código y documentación del Laboratorio 10
referencia/ORIGEN.txt   procedencia de la referencia
```

## Datos principales

- `flujo.csv`: ingresos mensuales por vía.
- `calendario.csv`: calendario mensual de enero de 2009 a junio de 2026.
- `metricas_modelos.csv`: MAE y RMSE de los modelos evaluados.
- `predicciones_lstm.csv`: valores observados y estimados por la LSTM.
- `metricas_lstm.csv`: configuración y métricas de las series LSTM.

