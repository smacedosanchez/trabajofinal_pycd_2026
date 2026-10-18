# trabajofinal_pycd_2026
Trabajo final del curso de Python para Ciencia de Datos de la Facultad de Ciencias Economicas y de Administracion.
Integrantes del grupo: Dylan Gandaria y Santiago Macedo.
# Trabajo final — Python para Ciencia de Datos 2026

**Sueño, uso de pantallas y rendimiento académico en estudiantes universitarios**

Autores: Santiago Macedo, Dylan Gandaria [agregar al tercer integrante si corresponde]

## Descripción

Análisis exploratorio y modelado del promedio académico (`cgpa`) de 500 estudiantes a partir de sus hábitos de sueño, uso de pantallas y estilo de vida. El trabajo incluye:

1. Revisión y limpieza de los datos.
2. Análisis exploratorio: distribución de la variable objetivo, relaciones con las demás variables y matriz de correlaciones.
3. Modelado: comparación de regresión lineal, árbol de decisión y Random Forest.
4. Una herramienta interactiva que estima el promedio y el percentil de un estudiante a partir de sus hábitos.

## Datos

- **Fuente:** [Student Sleep, Screen Time and Academic Performance (Kaggle)](https://www.kaggle.com/datasets/aamir28/student-sleep-screen-time-and-academic-performance)
- **Archivo:** `data/raw/data.csv` (500 observaciones, 25 variables)
- **Aclaración:** es un conjunto de datos simulado con fines educativos. Los resultados no describen estudiantes reales y no deben usarse para sacar conclusiones sobre ningún fenómeno del mundo real.

### Decisiones de limpieza

- **`gender`:** se unificaron las categorías duplicadas por escritura (`Female`/`female`/`F`, `Male`/`male`/`M`).
- **`bedtime_c`:** nueva variable que recodifica la hora de acostarse como horas respecto de la medianoche (por ejemplo, 23:00 pasa a -1), porque la escala original de 0 a 24 separa artificialmente horarios cercanos a la medianoche.
- **Modelado:** se eliminaron las filas con valores faltantes (de 500 quedan 478), una fila con asistencia mayor a 100 % que se descartó en el notebook como dato inválido y una con más de 60 horas semanales de estudio, que se trató como atípica. Quedan 477 observaciones.

## Resultados principales

Modelos evaluados sobre un 20 % de datos de prueba:

| Modelo | R² | RMSE | MAE |
|---|---|---|---|
| Regresión lineal | 0,286 | 0,265 | 0,214 |
| Random Forest | 0,279 | 0,266 | 0,211 |
| Árbol de decisión | 0,089 | 0,299 | 0,233 |

- La regresión lineal y el Random Forest rinden de forma similar, por lo que se prefiere la regresión lineal por ser más simple e interpretable.
- Las variables más importantes en los tres modelos son las horas de estudio semanales, la calidad del sueño y las horas de sueño entre semana.
- Todas las correlaciones individuales con `cgpa` son moderadas o débiles (ninguna supera 0,5), por lo que el poder predictivo es moderado.

## Estructura del repositorio

```
.
├── data/
│   ├── raw/             # datos originales sin modificar
│   └── processed/       # datos procesados
├── notebooks/
│   └── main.ipynb       # documento principal (análisis + código + texto)
├── requirements.txt     # dependencias
└── README.md
```

El documento final en formato [PDF / HTML] está en: [indicar ruta del archivo].

## Librerías utilizadas

| Librería | Uso en el trabajo |
|---|---|
| `numpy` | Operaciones numéricas y recodificación de variables |
| `pandas` | Carga, limpieza y manipulación de los datos |
| `matplotlib` | Gráficos base |
| `seaborn` | Visualizaciones (regresión por paneles, boxplots, histograma, heatmap) |
| `scikit-learn` | Partición de datos, modelos de regresión (lineal, árbol de decisión, Random Forest) y métricas |
| `ipywidgets` | Controles interactivos de la herramienta final |
| `ipython` | Visualización de tablas y HTML en el notebook |
| `jupyter` / `ipykernel` | Ejecución del notebook |

## Cómo reproducir el trabajo

1. Clonar el repositorio:
```
   git clone https://github.com/[usuario]/trabajofinal_pycd_2026.git
   cd trabajofinal_pycd_2026
```
2. Crear y activar un entorno. Ejemplo con conda:
```
   conda create -n pycd python=[versión] -y
   conda activate pycd
```
3. Instalar las dependencias:
```
   pip install -r requirements.txt
```
4. Abrir `notebooks/main.ipynb` y ejecutar todas las celdas en orden. El notebook lee los datos desde `data/raw/data.csv` (ruta relativa a la carpeta `notebooks/`).

**Nota:** la herramienta interactiva de la sección 4 usa `ipywidgets`, por lo que solo funciona al ejecutar el notebook; no se muestra interactiva en el PDF o HTML exportado.