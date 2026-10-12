# Tesis: Análisis Predictivo del Riesgo y Desempeño Financiero en SOFIPOs

El documento principal es `tesis_claude.tex`, que ahora solo contiene el preámbulo y una lista de `\input`. El contenido está dividido por partes para poder revisar o editar un capítulo sin abrir todo el archivo.

## Mapa del proyecto

| Archivo | Contenido | Líneas |
|---|---|---|
| `tesis_claude.tex` | Archivo maestro: preámbulo y orden de inclusión | 64 |
| `preliminares/portada_y_preliminares.tex` | Portada, dedicatoria, agradecimientos, resumen, abstract, abreviaturas, índices | 93 |
| `capitulos/cap01_introduccion.tex` | Capítulo 1. Introducción y marco de contexto | 50 |
| `capitulos/cap02_marco_teorico.tex` | Capítulo 2. Marco teórico | 995 |
| `capitulos/cap03_metodologia.tex` | Capítulo 3. Marco metodológico | 625 |
| `capitulos/cap04_arquitectura.tex` | Capítulo 4. Arquitectura computacional del sistema | 37 |
| `capitulos/cap05_analisis_exploratorio.tex` | Capítulo 5. Análisis exploratorio de datos | 60 |
| `capitulos/cap06_resultados.tex` | Capítulo 6. Resultados de los modelos | 153 |
| `capitulos/cap07_discusion.tex` | Capítulo 7. Discusión de resultados | 11 |
| `capitulos/cap08_alerta_temprana.tex` | Capítulo 8. Sistema de alerta temprana | 12 |
| `capitulos/cap11_conclusiones.tex` | Capítulo 11. Conclusiones y recomendaciones | 9 |
| `bibliografia/bibliografia.tex` | Referencias (APA 7ª edición) | 113 |
| `bibliografia/glosario.tex` | Glosario | 24 |
| `anexos/anexo_A_fragmentos.tex` | Anexo A. Fragmentos comentados del pipeline | 37 |
| `anexos/anexo_B_metricas.tex` | Anexo B. Métricas reproducidas | 22 |
| `anexos/anexo_C_codigo.tex` | Anexo C. Código completo del pipeline | 7 |

Para cambiar el orden de los capítulos o agregar uno nuevo, edita la lista de `\input` en `tesis_claude.tex`.

## Compilación

Se necesitan dos elementos que no están en el repositorio: la carpeta `figuras/` (fig01 a fig17 y `fig_ishikawa_mejorado.png`) y el archivo `PORTADA.pdf`. Después, compila dos veces con pdfLaTeX:

```
pdflatex -interaction=nonstopmode tesis_claude.tex
pdflatex -interaction=nonstopmode tesis_claude.tex
```

## Notas

- El anexo C incluye el script `ejecutar_pipeline_completo_ascii.py` con `\lstinputlisting`. Ese archivo debe estar en la misma carpeta que el `.tex` para compilar.
- Las partes se dividieron a partir de la versión anterior de `tesis_claude.tex`. Después de la división se ampliaron y actualizaron como se describe en la sección "Cambios de esta versión".
- El anexo C requiere que el script `.py` esté en la carpeta del `.tex`. Ese script no está en el repositorio.
- Los capítulos 9 y 10 se eliminaron. La numeración de los demás capítulos de este mapa conserva los nombres de archivo originales.

## Seguridad: token de Banxico

Por cuestiones de seguridad, el token de la API del Sistema de Información Económica de Banco de México no se agrega a este repositorio. Los archivos `*.py`, `*.txt` y `*.json` están en el `.gitignore` precisamente para que el token, los datos y las salidas locales no se publiquen.

Para ejecutar el pipeline en tu computadora, el script `ejecutar_pipeline_completo_ascii.py` busca el token en este orden:

1. La variable de entorno `BANXICO_TOKEN`.
2. El archivo local `api.txt`, que debe contener el token de 64 caracteres y no se versiona.

Si la descarga desde la API falla, el pipeline se detiene con un error. No existe un respaldo con series simuladas.

## Ejecución del pipeline y figuras

Las figuras se generan con matplotlib a 350 puntos por pulgada (`figure.dpi` y `savefig.dpi`), y el diagrama de Ishikawa también. Se necesitan los paquetes `numpy`, `pandas`, `polars`, `duckdb`, `pyarrow`, `matplotlib`, `xgboost`, `lightgbm`, `scikit-learn`, `statsmodels`, `shap`, `imbalanced-learn` y `requests`. Con las versiones actuales, `shap` requiere NumPy 2.2 o anterior y el script requiere Polars anterior a la versión 2.

```
pip install "numpy<2.3" pandas "polars<2" duckdb pyarrow requests scikit-learn xgboost lightgbm statsmodels shap imbalanced-learn matplotlib
python ejecutar_pipeline_completo_ascii.py
```

El script lee `sofipo_base_completa.parquet` desde la misma carpeta, escribe las 17 figuras en `figuras/` y las métricas en `resultados_metricas.json`. Esas salidas no se versionan.

## Cambios de esta versión

### Estructura del documento

- Se eliminaron los capítulos 9 y 10, la guía de defensa y el Anexo D (código original `codigo_unificado_gemini`).
- Los títulos de los capítulos son "Marco Teórico" y "Marco Metodológico". No se cambiaron los demás títulos.
- Se usa el paquete `lmodern` para que el PDF tenga fuentes vectoriales. Sin él, MiKTeX generaba fuentes de mapa de bits (Type 3) que se veían borrosas al hacer zoom.

### Marco Teórico (capítulo 2)

Se amplió de lo más sencillo a lo más avanzado, con definición intuitiva, definición formal, ejemplo numérico ilustrativo y la razón por la que se usa en la tesis. El orden es:

1. Fundamentos matemáticos y estadísticos: probabilidad, variables aleatorias, distribuciones, estimadores, máxima verosimilitud, mínimos cuadrados, correlación, valores atípicos, bootstrap, contrastes de hipótesis y regresión logística.
2. Fundamentos de programación y manejo de datos: ecosistema de Python, formato Parquet, SQL con funciones de ventana, ETL, API REST, complejidad computacional y resolución de imagen en dpi.
3. Estados financieros y variables contables de una SOFIPO: balance, estado de resultados línea por línea, cada partida que usa el código, indicadores (ROA, ROE, eficiencia, costo de riesgo, apalancamiento, DuPont) y un ejemplo numérico completo.
4. Variables macroeconómicas: inflación e INPC, tasas nominal y real, TIIE, Cetes, tipo de cambio FIX e IGAE, y el procedimiento exacto del código.
5. Microfinanzas y riesgo crediticio.
6. Econometría de panel y series de tiempo.
7. Optimización matemática y computacional: descenso por gradiente, SGD, Adam, búsqueda de hiperparámetros y programación dinámica.
8. Aprendizaje automático supervisado, preparación de datos de panel, validación temporal, desbalance, métricas, interpretabilidad con Shapley y limitaciones del estudio.

### Marco Metodológico (capítulo 3)

Se reescribió desde cero siguiendo el orden real del pipeline: datos, limpieza con SQL, rezagos y medias móviles, objetivos, partición, modelos, métricas, figuras, amenazas a la validez y reproducción paso a paso. Corrige la afirmación anterior de que la partición era cronológica: el código usa `shuffle=False` sobre un panel ordenado por institución, lo que no separa periodos.

### Bibliografía

Se agregaron 61 fuentes en formato APA 7, con DOI verificado en CrossRef y arXiv: Nature (LeCun et al., Scheffer et al., Harris et al.), Nature Machine Intelligence (Rudin), Nature Methods (Virtanen et al.), arXiv (Kingma y Ba, Ruder, Grinsztajn et al., Guo et al., Prokhorenkova et al., Snoek et al.) y revistas de finanzas y de ciencia de datos. Las que no se pudieron verificar quedaron con `% VERIFICAR`.

### Resultados

El pipeline se ejecutó con las series macroeconómicas oficiales de la API SIE de Banco de México. La ejecución anterior usaba series sintéticas deterministas y se descartó; queda documentada como antecedente. Se actualizaron las cifras en los capítulos 1 a 7 y 11, el resumen, el abstract y el anexo B.

| Métrica | Ejecución anterior (series sintéticas) | Ejecución actual (series oficiales) |
|---|---|---|
| XGBoost R² | 0.6126 | 0.6272 |
| XGBoost MAE | 3.29 | 3.16 |
| XGBoost RMSE | 7.97 | 7.81 |
| Exactitud | 88.65 % | 88.24 % |
| Precisión | 70.00 % | 69.49 % |
| Sensibilidad | 82.35 % | 80.39 % |
| F1 | 0.7568 | 0.7455 |
| ROC-AUC | 0.9148 | 0.9227 |
| MCC | 0.6873 | 0.6725 |

LightGBM, Random Forest y los benchmarks ARIMA y SARIMA no cambian porque no usan variables macroeconómicas. En el ranking SHAP, el IGAE encabeza ahora las variables macroeconómicas y los Cetes dejan de tener contribución cero.

### Figuras

Las 17 figuras y el diagrama de Ishikawa se generan a 350 dpi. Una figura de 8 por 4.5 pulgadas mide 2800 por 1575 píxeles.

### Pendientes y límites conocidos

- La partición entrenamiento y prueba no es cronológica por periodo.
- La imputación con el promedio por institución usa información futura.
- SMOTE-ENN se aplica antes de la validación cruzada del stacking, y esa validación no es temporal.
- La selección del mejor modelo multiobjetivo se hace con el conjunto de prueba.
- El umbral de 10 % del IMOR para definir Default es una decisión de diseño sin fuente.
- El SARIMA del código usa estacionalidad de 12 periodos aunque el panel es trimestral.
- `IMOR_futuro` y `target_IMOR 1/ (%)` son la misma columna.
- La curva de XGBoost de la Figura 16 se evalúa también sobre filas que pudieron estar en el entrenamiento.
- Después de unir las variables macroeconómicas no se revisan valores faltantes.
- El ROA del código usa el activo de cierre y no está anualizado.
- `warnings.filterwarnings("ignore")` oculta avisos de convergencia de statsmodels.
- Quedan líneas marcadas con `% VERIFICAR` en los capítulos 2 y 3 y en la bibliografía, por ejemplo la definición de "tasa implícita" del boletín de la CNBV.
