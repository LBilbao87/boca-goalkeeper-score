# Boca Goalkeeper Score

Proyecto de análisis de datos orientado a evaluar posibles arqueros para Boca Juniors utilizando métricas de rendimiento de la temporada 2026 en Argentina y Brasil.

## Resumen

Este proyecto parte de una pregunta concreta:

> ¿Existe en Argentina o Brasil un arquero claramente superior a Leandro Brey según los datos disponibles?

La intención no es construir una recomendación definitiva de scouting, sino desarrollar una primera herramienta analítica, simple e interpretable, para comparar perfiles de arqueros y detectar candidatos que ameriten un análisis más profundo.

## Pregunta analítica

**¿Hay una opción externa que, según métricas seleccionadas, se destaque claramente por encima de Leandro Brey?**

## Fuente de datos

El análisis utiliza datos de arqueros exportados desde FBref para la temporada 2026.

Archivos esperados:

```text
argentina_keepers_2026.csv
argentina_keepers_advanced_2026.csv
brazil_keepers_2026.csv
brazil_keepers_advanced_2026.csv
```

Se utilizan tablas estándar y avanzadas de arqueros de Argentina y Brasil.

## Metodología

El notebook sigue estos pasos:

1. Carga de archivos CSV exportados desde FBref.
2. Limpieza y normalización de tablas.
3. Unión de datos estándar y avanzados.
4. Aplicación de filtros de candidatos.
5. Construcción de un score compuesto.
6. Ranking de arqueros.
7. Visualización de resultados.

## Filtros aplicados

| Filtro | Criterio | Objetivo |
|---|---:|---|
| Edad | ≤ 34 | Excluir arqueros en una etapa final de carrera |
| Minutos jugados | ≥ 300 | Evitar muestras demasiado pequeñas |

Estos filtros buscan mantener el análisis enfocado en perfiles mínimamente representativos y potencialmente realistas.

## Boca GK Score v1

El proyecto construye un índice propio llamado **Boca GK Score v1**.

Las variables son escaladas entre 0 y 1 mediante MinMaxScaler antes de aplicar las ponderaciones.

| Métrica | Peso | Dirección | Justificación |
|---|---:|---|---|
| Porcentaje de atajadas | 45% | Mayor es mejor | Principal indicador de shot-stopping |
| Goles recibidos cada 90 minutos | 20% | Menor es mejor | Penaliza arqueros que reciben goles con mayor frecuencia |
| Porcentaje de vallas invictas | 15% | Mayor es mejor | Premia resultados defensivos |
| Minutos jugados | 10% | Mayor es mejor | Valora continuidad y confianza del cuerpo técnico |
| Atajadas cada 90 minutos | 5% | Mayor es mejor | Captura volumen de intervención |
| Perfil de edad | 5% | Pico entre 24 y 31 | Premia levemente edades consideradas óptimas para el puesto |

El score es deliberadamente simple e interpretable. Está pensado como una primera versión que puede ser mejorada con mayor contexto táctico, información contractual, ajuste por liga y validación cualitativa.

## Outputs

El notebook genera:

- Un ranking de candidatos.
- Una tabla final comparativa.
- Un mapa de perfiles según porcentaje de atajadas y goles recibidos cada 90 minutos.
- Un gráfico de top 10 según el Boca GK Score v1.

## Herramientas utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

## Reproducibilidad

Para reproducir el análisis:

1. Descargar los archivos CSV correspondientes desde FBref.
2. Ubicarlos en la ruta esperada por el notebook o cargarlos en Google Colab.
3. Abrir el notebook:

```text
notebooks/01_boca_goalkeeper_score.ipynb
```

4. Ejecutar todas las celdas.

## Disponibilidad de los datos

Los archivos originales no se incluyen necesariamente en el repositorio, ya que pueden estar sujetos a restricciones de redistribución de la fuente.

Para reproducir el análisis, se recomienda descargar los datos originales desde FBref y ubicarlos con los nombres esperados.

## Limitaciones

Este proyecto debe interpretarse como un ejercicio exploratorio de análisis de datos, no como un informe completo de scouting.

Principales limitaciones:

- El score depende de las métricas disponibles.
- No se ajusta completamente por contexto de equipo.
- No se ajusta por nivel relativo de liga.
- No se modela directamente el rol táctico del arquero.
- No se incluyen contrato, salario ni valor de mercado.
- No se incorpora scouting cualitativo.
- Las métricas avanzadas de shot-stopping pueden integrarse mejor en futuras versiones.

## Próximos pasos

Posibles mejoras:

- Incorporar PSxG+/- y métricas avanzadas al score.
- Ajustar rendimiento por contexto de equipo y liga.
- Agregar edad, contrato y valor de mercado.
- Incluir más ligas.
- Construir perfiles por percentiles.
- Comparar candidatos contra perfiles históricos de arqueros de Boca.
- Sumar notas cualitativas de scouting.
- Automatizar exportación de tablas y gráficos.

## Disclaimer

Este proyecto es un ejercicio analítico independiente y no está afiliado a Boca Juniors, FBref ni a ninguna organización deportiva.

El análisis tiene fines educativos, de portfolio y de análisis deportivo.
