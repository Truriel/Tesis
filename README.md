# Tesis: Análisis Predictivo del Riesgo y Desempeño Financiero en SOFIPOs

El documento principal es `tesis_claude.tex`, que ahora solo contiene el preámbulo y una lista de `\input`. El contenido está dividido por partes para poder revisar o editar un capítulo sin abrir todo el archivo.

## Mapa del proyecto

| Archivo | Contenido | Líneas |
|---|---|---|
| `tesis_claude.tex` | Archivo maestro: preámbulo y orden de inclusión | 77 |
| `preliminares/portada_y_preliminares.tex` | Portada, dedicatoria, agradecimientos, resumen, abstract, abreviaturas, índices | 87 |
| `capitulos/cap01_introduccion.tex` | Capítulo 1. Introducción y marco de contexto | 67 |
| `capitulos/cap02_marco_teorico.tex` | Capítulo 2. Marco teórico | 1356 |
| `capitulos/cap03_metodologia.tex` | Capítulo 3. Marco metodológico | 83 |
| `capitulos/cap04_arquitectura.tex` | Capítulo 4. Arquitectura computacional del sistema | 43 |
| `capitulos/cap05_analisis_exploratorio.tex` | Capítulo 5. Análisis exploratorio de datos | 73 |
| `capitulos/cap06_resultados.tex` | Capítulo 6. Resultados de los modelos | 174 |
| `capitulos/cap07_discusion.tex` | Capítulo 7. Discusión de resultados | 17 |
| `capitulos/cap08_alerta_temprana.tex` | Capítulo 8. Sistema de alerta temprana | 15 |
| `capitulos/cap11_conclusiones.tex` | Capítulo 11. Conclusiones y recomendaciones | 13 |
| `bibliografia/bibliografia.tex` | Referencias (APA 7ª edición) | 41 |
| `bibliografia/glosario.tex` | Glosario | 14 |
| `anexos/anexo_A_fragmentos.tex` | Anexo A. Fragmentos comentados del pipeline | 44 |
| `anexos/anexo_B_metricas.tex` | Anexo B. Métricas reproducidas | 24 |
| `anexos/anexo_C_codigo.tex` | Anexo C. Código completo del pipeline | 10 |

Para cambiar el orden de los capítulos o agregar uno nuevo, edita la lista de `\input` en `tesis_claude.tex`.

## Compilación

Se necesitan dos elementos que no están en el repositorio: la carpeta `figuras/` (fig01 a fig17 y `fig_ishikawa_mejorado.png`) y el archivo `PORTADA.pdf`. Después, compila dos veces con pdfLaTeX:

```
pdflatex -interaction=nonstopmode tesis_claude.tex
pdflatex -interaction=nonstopmode tesis_claude.tex
```

## Notas

- El anexo C incluye el script `ejecutar_pipeline_completo_ascii.py` con `\lstinputlisting`. Ese archivo debe estar en la misma carpeta que el `.tex` para compilar.
- El texto de cada parte es idéntico a la versión anterior de `tesis_claude.tex`. Solo se hicieron dos correcciones necesarias para compilar: se eliminó un `\begin{thebibliography}{99}` duplicado y se escaparon las `&` de las referencias (`\&`).
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
