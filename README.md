# Store Item Demand Forecasting

Análisis de datos y predicción de ventas para 10 tiendas y 50 productos.  
Proyecto personal de práctica en Data Science.

---

## Descripción del problema

Mi objetivo es predecir cuántas unidades se van a vender de cada producto en cada tienda durante los primeros 3 meses de 2018, usando datos históricos de kaggle de 2013 a 2017.

Es un problema de **series temporales** con componentes de:
- Tendencia (las ventas crecen año a año)
- Estacionalidad (hay meses que venden más que otros)
- Variabilidad por tienda e ítem

## Estructura del proyecto

```
store-sales-forecasting/
├── analisis_ventas.ipynb    # Notebook principal con todo el análisis
├── train.csv                # Datos de entrenamiento (2013-2017)
├── test.csv                 # Datos de test (2018 Q1)
├── sample_submission.csv    # Ejemplo del formato de entrega
├── submission.csv           # Mis predicciones finales
└── README.md
```

## Qué contiene el análisis

El notebook recorre todo el proceso desde cero:

1. **Carga y exploración de datos** - entender qué tenemos antes de tocar nada
2. **Feature engineering** - extraer año, mes, día de la semana de las fechas
3. **Visualizaciones** - gráficos de estacionalidad, evolución anual, heatmaps...
4. **Modelo de predicción** - mediana por tienda/ítem/mes con datos 2016-2017
5. **Validación** - comprobando el error en 2017 antes de predecir 2018
6. **Generación del submission**

## Algunos resultados del EDA

- El dataset tiene **913.000 filas** (5 años × 365 días × 10 tiendas × 50 ítems)
- Ventas medias: ~52 unidades/día, con mucha variabilidad entre productos
- Las ventas suben en verano y tienen un patrón semanal claro
- Los ítems tienen rendimientos muy distintos (algunos venden 10x más que otros)

## Modelo utilizado

He elegido/optado por un enfoque basado en **mediana histórica por grupo** (store + item + mes), usando solo los datos de 2016-2017 por ser los más representativos del comportamiento reciente.

**Resultados de validación (en año 2017):**
| Métrica | Valor |
|---------|-------|
| MAE | ~8.2 |
| RMSE | ~11.1 |
| SMAPE | ~15.8% |

No es el modelo más sofisticado del mundo, pero como primer proyecto de series temporales estoy bastante contento con el resultado.

## Requisitos

```
pandas
numpy
matplotlib
seaborn
```

Instalación rápida:
```bash
pip install pandas numpy matplotlib seaborn
```

## Cómo ejecutar

```bash
# clonar el repositorio
git clone https://github.com/[tu-usuario]/store-sales-forecasting.git
cd store-sales-forecasting

# abrir el notebook
jupyter notebook analisis_ventas.ipynb
```

## Qué mejorar :))

- Probar modelos de ML (Random Forest, XGBoost, LightGBM)
- Usar Prophet o SARIMA para modelar la serie temporal de verdad
- Añadir información de festivos que probablemente impacta mucho
- Cross-validation más rigurosa con ventana deslizante

---

*Dataset original de [Kaggle - Store Item Demand Forecasting Challenge](https://www.kaggle.com/c/demand-forecasting-kernels-only)*  
*Proyecto realizado como práctica personal — David López, Universitat de Barcelona*
