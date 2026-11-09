# Laboratorio 12 - Power BI

Segunda versión del observatorio del flujo turístico a Guatemala. Usamos los mismos datos, preguntas y resultados de modelos del Laboratorio 10, ahora en Power BI Desktop.

https://github.com/UVG-Tareas-y-proyectos/LAB12_DS

## Archivos de entrega

- `Observatorio.pbix`: informe final de Power BI con los datos cargados.
- `docs/informe_final_lab12.pdf`: documento de diseño y comparación de herramientas.
- `docs/informe_final_lab12.docx`: versión editable del documento.
- `powerbi/Observatorio.pbip`: el mismo informe como proyecto PBIP, para ver los cambios en Git.
- `avance_lab12.pdf` y `avance_lab12.docx`: documento del avance.

La versión del informe que entregamos en el avance (v0.1, 5 de noviembre) está en el commit `ccc22a3`.

## Versión de Power BI

Power BI Desktop 2.159.1231.0 de 64 bits, instalado desde Microsoft Store en Windows 11. Power BI Desktop solo funciona en Windows.

## Estructura

```text
Observatorio.pbix       informe de Power BI
powerbi/                proyecto PBIP (Observatorio.Report y Observatorio.SemanticModel)
data/raw/               fuentes originales: Excel de migración y resultados de modelos
data/processed/         CSV que carga Power BI e indicadores de control
docs/                   documento final, registro de pruebas y de tiempos
docs/evidencias/        capturas de las dos versiones
referencia/lab10/       código, datos y documento del Laboratorio 10
referencia/ORIGEN.txt   de dónde sale la copia del Lab 10
avance_lab12.*          documento del avance
```

## Cómo abrir el informe

Abrir `Observatorio.pbix` con Power BI Desktop. Los datos ya vienen cargados, así que se puede revisar sin actualizar nada.

Para volver a cargar los datos desde los CSV:

1. Ir a Home, Transform data, Edit parameters (en español: Inicio, Transformar datos, Editar parámetros).
2. Cambiar `RutaDatos` por la ruta completa de la carpeta `data/processed` en su computadora, por ejemplo `C:/Users/usuario/LAB12_DS/data/processed`, sin barra al final.
3. Aplicar los cambios y darle a Refresh. Son 11 tablas y tarda menos de un minuto.

El proyecto `powerbi/Observatorio.pbip` se abre de la misma forma. La primera vez Power BI muestra un aviso para actualizar; hay que cambiar `RutaDatos` y luego darle a Refresh now.

Los CSV salen del proceso de preparación del Lab 10 (`referencia/lab10/src/preparar_datos.py`). Si se vuelven a generar, hay que copiarlos a `data/processed`. Los totales para comprobar la carga están en `data/processed/indicadores_control.json`.

## Tablas

Tablas de predicciones y métricas:

- `Metricas` (`metricas_modelos.csv`): MAE y RMSE de los 8 modelos del Lab 1 sobre la serie Total mensual.
- `MetricasLSTM` (`metricas_lstm.csv`): MAE, RMSE y sMAPE de la LSTM del Lab 2.
- `Predicciones` (`predicciones_lstm.csv`): valor observado y estimado por la LSTM, por serie y mes.

Estas tres tablas no están relacionadas con el calendario, para que los filtros de fechas no cambien resultados de pruebas que ya se hicieron.

Las demás tablas son `Calendario`, `Vias`, `Region`, `Flujo`, `Regiones`, `Mercados`, `Fronteras` e `IndiceEstacional`. El detalle de cada una está en el documento final.

## Páginas

- Exploración: indicadores, serie temporal (se puede bajar de año a trimestre y a mes) y barras por vía que cambian al seleccionar un punto de la serie.
- Mercados y acceso: regiones, países y puntos de ingreso. Al hacer clic en una línea de regiones se filtran los países.
- Estacionalidad y modelos: índice estacional, error de los modelos del Lab 1 y resultados de la LSTM.
- Guía y límites: preguntas de gestión, colores, fuente y restricciones de los datos.

Los botones de arriba cambian de página y el botón Limpiar filtros quita lo seleccionado en los segmentadores.

## Las tres pruebas

Antes de cada prueba darle a Limpiar filtros y hacer clic en un espacio vacío. Anotar resultado, clics, segundos y dificultades en `docs/pruebas_comparacion.csv`.

1. Consulta con filtros: en Exploración elegir Año 2019 y los meses Ene a Jun. Debe dar 2,023,752 ingresos y 64.70 % terrestre.
2. De lo general al detalle y regreso: en la serie de Exploración activar el modo drill (flecha hacia abajo en la esquina de la gráfica), hacer clic en 2014, luego en T4 y luego en Dic, y ver las barras por vía. Regresar con la flecha hacia arriba dos veces. Debe dar Aérea 117,878, Marítima 1,140 y Terrestre 206,355.
3. Modelos: en Estacionalidad y modelos elegir Grupo de modelos = Simple de referencia y Serie LSTM = Total mensual de viajeros. El menor RMSE es el de Suavizamiento exponencial simple, 180,598.

## Versión del Laboratorio 10

Necesita Python 3.11 o más reciente. Desde `referencia/lab10`:

```powershell
python -m venv .venv
.venv\Scripts\python.exe -m pip install -r requirements.txt
.venv\Scripts\python.exe -m src.preparar_datos
.venv\Scripts\python.exe -m streamlit run app.py
```

Las mismas pruebas en Streamlit: (1) periodo 2019-2019 y meses 1 a 6; (2) nivel Mensual y clic en el punto de diciembre de 2014; (3) pestaña Estacionalidad y modelos con RMSE.

## Fuente y limitaciones

Base académica `Base_Migracion_2009-2026jun.xlsx`, hoja Datos. Se suman Turista y Excursionista. Las cifras son ingresos registrados, no personas. 2020 y 2021 son atípicos, desde 2023 cambia la metodología, desde 2017 hay menos detalle marítimo y 2026 solo tiene enero a junio. No entrenamos modelos nuevos.
