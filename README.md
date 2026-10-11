# Tesis: Análisis Predictivo del Riesgo y Desempeño Financiero en SOFIPOs

El documento principal es `tesis_claude.tex`, que ahora solo contiene el preámbulo y una lista de `\input`. El contenido está dividido por partes para poder revisar o editar un capítulo sin abrir todo el archivo.

## Mapa del proyecto

| Archivo | Contenido | Líneas |
|---|---|---|
| `tesis_claude.tex` | Archivo maestro: preámbulo y orden de inclusión | 77 |
| `preliminares/portada_y_preliminares.tex` | Portada, dedicatoria, agradecimientos, resumen, abstract, abreviaturas, índices | 87 |
| `capitulos/cap01_introduccion.tex` | Capítulo 1. Introducción y marco de contexto | 67 |
| `capitulos/cap02_marco_teorico.tex` | Capítulo 2. Marco teórico integral | 108 |
| `capitulos/cap03_metodologia.tex` | Capítulo 3. Marco metodológico | 83 |
| `capitulos/cap04_arquitectura.tex` | Capítulo 4. Arquitectura computacional del sistema | 43 |
| `capitulos/cap05_analisis_exploratorio.tex` | Capítulo 5. Análisis exploratorio de datos | 73 |
| `capitulos/cap06_resultados.tex` | Capítulo 6. Resultados de los modelos | 174 |
| `capitulos/cap07_discusion.tex` | Capítulo 7. Discusión de resultados | 17 |
| `capitulos/cap08_alerta_temprana.tex` | Capítulo 8. Sistema de alerta temprana | 15 |
| `capitulos/cap09_implementacion.tex` | Capítulo 9. Implementación y aplicación práctica | 9 |
| `capitulos/cap10_comparativa_trabajo_futuro.tex` | Capítulo 10. Comparativa internacional y trabajo futuro | 16 |
| `capitulos/cap11_conclusiones.tex` | Capítulo 11. Conclusiones y recomendaciones | 13 |
| `bibliografia/bibliografia.tex` | Referencias (APA 7ª edición) | 41 |
| `bibliografia/glosario.tex` | Glosario | 14 |
| `anexos/guia_defensa.tex` | Guía de preguntas para la defensa | 43 |
| `anexos/anexo_A_fragmentos.tex` | Anexo A. Fragmentos comentados del pipeline | 44 |
| `anexos/anexo_B_metricas.tex` | Anexo B. Métricas reproducidas | 24 |
| `anexos/anexo_C_codigo.tex` | Anexo C. Código completo del pipeline | 10 |
| `anexos/anexo_D_codigo_original.tex` | Anexo D. Código original del proyecto | 5 |

Para cambiar el orden de los capítulos o agregar uno nuevo, edita la lista de `\input` en `tesis_claude.tex`.

## Compilación

Se necesitan dos elementos que no están en el repositorio: la carpeta `figuras/` (fig01 a fig17 y `fig_ishikawa_mejorado.png`) y el archivo `PORTADA.pdf`. Después, compila dos veces con pdfLaTeX:

```
pdflatex -interaction=nonstopmode tesis_claude.tex
pdflatex -interaction=nonstopmode tesis_claude.tex
```

## Notas

- Los anexos C y D incluyen los scripts `ejecutar_pipeline_completo_ascii.py` y `codigo_unificado_gemini_ascii.py` con `\lstinputlisting`. Esos archivos deben estar en la misma carpeta que el `.tex` para compilar.
- El texto de cada parte es idéntico a la versión anterior de `tesis_claude.tex`. Solo se hicieron dos correcciones necesarias para compilar: se eliminó un `\begin{thebibliography}{99}` duplicado y se escaparon las `&` de las referencias (`\&`).
- Los anexos C y D requieren que los scripts `.py` estén en la carpeta del `.tex`. Esos scripts no están en el repositorio.
