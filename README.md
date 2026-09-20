# Movilidad urbana y productividad económica en Latinoamérica

Análisis exploratorio con **Python (pandas, matplotlib, seaborn)** sobre la relación entre la congestión vehicular y el PIB per cápita en ciudades de Latinoamérica, integrando datos de movilidad (TomTom Traffic Index) e indicadores económicos (OECD Cities) del año 2024.

---

## Contexto del problema

La pregunta de negocio central fue: **¿existe una relación entre la movilidad urbana (congestión, tiempos de viaje) y la productividad económica (PIB per cápita) de una ciudad?** Responderla es relevante para decidir en qué ciudades conviene invertir en infraestructura de transporte, bajo la hipótesis de que reducir la congestión podría tener mayor impacto económico en algunos mercados que en otros.

---

## Herramientas utilizadas

| Herramienta | Uso en el proyecto |
|---|---|
| **Python** | Lenguaje principal del análisis |
| **pandas** | Limpieza, transformación, agregación y unión (merge) de datasets |
| **NumPy** | Soporte para operaciones numéricas |
| **Matplotlib / Seaborn** | Visualización: boxplot, histograma, gráfico de barras y dispersión |
| Jupyter Notebook | Entorno de desarrollo y documentación del análisis |

---

## Fuentes de datos

- **TomTom Traffic Index**: métricas diarias de congestión por ciudad (retraso en minutos, longitud de embotellamientos, tiempos de viaje).
- **OECD Cities**: indicadores económicos por ciudad (PIB per cápita, tasa de desempleo, población, calidad del aire).

---

## Metodología

1. **Exploración inicial.** Revisión de estructura, tipos de dato y valores faltantes en ambos datasets.
2. **Limpieza y estandarización.** Conversión de columnas de fecha a `datetime`, limpieza de campos numéricos con formato europeo (separadores de miles y decimales), y estandarización de nombres de columna a `snake_case` para facilitar la unión de tablas.
3. **Filtrado temporal.** Se extrajo el año de cada registro y se limitó el análisis al periodo 2024.
4. **Agregación.** Los datos de tráfico, con múltiples registros diarios por ciudad, se resumieron en promedios anuales por ciudad y país.
5. **Unión de datasets (inner join).** Se combinaron los indicadores de movilidad y económicos por ciudad y año, conservando únicamente las ciudades con información completa en ambas fuentes — de 387 ciudades con datos de tráfico, solo 15 contaban con datos económicos completos, lo cual se documentó como una limitación explícita del alcance.
6. **Visualización.** Boxplot, histograma, gráfico de barras y de dispersión para identificar distribución, outliers y posibles relaciones entre variables.

---

## Hallazgos principales

- **No se encontró una relación consistente** entre el PIB per cápita y el tiempo de retraso por tráfico. Montevideo combina el PIB per cápita más alto con uno de los menores tiempos de congestión, mientras que Ciudad de México combina un PIB per cápita alto con el mayor tiempo de retraso de toda la muestra.
- **Ciudad de México es un valor atípico (outlier)**: registra 2,833 minutos de retraso promedio, **10.8 veces mayor** que la mediana del grupo (263 minutos), además de concentrar ~22.1 millones de habitantes y una tasa de desempleo baja (3.2%).
- Fortaleza y El Salvador se ubican entre las ciudades con **menor** congestión y también entre las de **menor** PIB per cápita, reforzando que no hay un patrón único entre ambas variables.
- El alcance del estudio quedó limitado a **15 ciudades de 7 países** tras el cruce de ambas fuentes, lo que se señala explícitamente como una limitación para generalizar los resultados.

---

## Recomendaciones

- **Ciudad de México** es la principal candidata de inversión en infraestructura vial: combina una población considerablemente alta, baja tasa de desempleo y el mayor nivel de congestión de la muestra, lo que sugiere un impacto económico potencialmente alto si se mejora la movilidad.
- **Santiago** aparece como segunda alternativa: presenta una combinación atípica de PIB per cápita relativamente bajo y tiempos de congestión elevados frente a ciudades de actividad económica similar, lo que podría representar una oportunidad de inversión con proyección de crecimiento económico.
- Se recomienda ampliar la cobertura de datos económicos a más ciudades del dataset de tráfico (solo 15 de 387 tenían información completa) antes de sacar conclusiones definitivas sobre la correlación entre ambas variables.

---

## Archivos del repositorio

```
├── notebook/
│   └── movilidad_economia_latam.ipynb   # Notebook completo con código, gráficos y análisis
└── README.md
```

> Nota: el CSV consolidado (`ladb_mobility_economy_2024_clean.csv`) que genera el notebook no se incluye en este repositorio por no contar con los datasets de origen completos; el notebook documenta el proceso de principio a fin y los gráficos ya están guardados dentro de él.

---

## Habilidades demostradas

- Limpieza y transformación de datos con pandas (tipos de dato, formatos numéricos regionales, fechas)
- Unión de múltiples fuentes de datos y manejo explícito de las limitaciones de cobertura resultantes
- Agregación de series temporales a nivel de resumen anual
- Visualización exploratoria de datos (distribución, outliers, relaciones entre variables)
- Interpretación crítica de resultados: distinguir correlación aparente de relación real, y documentar limitaciones del alcance del estudio
- Traducción de hallazgos analíticos en recomendaciones de inversión priorizadas
