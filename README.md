# 🌍 Forecasting en series temporales de contaminantes atmosféricos en Madrid (2001-2018)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Time Series](https://img.shields.io/badge/time--series-analysis-blue)](https://en.wikipedia.org/wiki/Time_series)
[![ARIMA](https://img.shields.io/badge/ARIMA-forecasting-red)](https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average)
![Visitas](https://komarev.com/ghpvc/?username=SebastianDeghi&repo=seoul-air-pollution-time-series-analysis&color=blue&style=flat)

### 👥 Colaboradores: **David Abba, Eduardo Andreozzi, Pablo Astoreca y Eduardo Castro Luna.**

***

## 📝 Descripción General

Análisis y predicción de series temporales de contaminantes atmosféricos (NO₂ y CO) en la ciudad de Madrid durante el período 2001-2018. El proyecto incluye limpieza de datos, análisis de estacionariedad (tests ADF y KPSS), descomposición estacional, transformación Box-Cox, diferenciación, y aplicación de modelos ARIMA y suavizado exponencial (SES, Holt, Holt-Winters) para pronóstico.

***

## 📁 Estructura del Proyecto

La organización de los archivos en este repositorio es la siguiente:

```
madrid-air-pollution-time-series-forecasting/
├── Madrid_Air_Pollution_Forecasting.ipynb   # Notebook principal
├── requirements.txt                         # Dependencias de Python
├── LICENSE                                  # Licencia MIT
├── .gitignore                               # Archivos ignorados
└── README.md                                # Este archivo
```

***

## 📊 Dataset

**Fuente:** [Air Quality in Madrid (2001-2018)](https://www.kaggle.com/datasets/decide-soluciones/air-quality-madrid) en Kaggle  
**Autor:** decide-soluciones  
**Fuente original:** Ayuntamiento de Madrid (Open Data)  
**Licencia:** Open Data (uso libre con atribución)

### Características del Dataset

| Característica | Descripción |
|----------------|-------------|
| **Período** | 2001 - 2018 (18 años) |
| **Frecuencia** | Mediciones horarias |
| **Contaminantes** | NO₂ (µg/m³), CO (mg/m³) |
| **Estructura** | Archivos CSV anuales (madrid_2001.csv a madrid_2018.csv) |
| **Estaciones** | Múltiples estaciones de monitoreo en Madrid |

## 🔧 Instalación y Uso

### 1. Clonar el repositorio

```bash
git clone https://github.com/SebastianDeghi/madrid-air-pollution-time-series-forecasting.git
cd madrid-air-pollution-time-series-forecasting
```

### 2. Crear y activar un entorno virtual (recomendado)

- En **Windows**:
  ```bash
  python -m venv venv
  venv\Scripts\activate
  ```
- En **macOS/Linux**:
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```

### 3. Instalar dependencias

Con el entorno virtual activo, instala los paquetes necesarios:
```bash
pip install -r requirements.txt
```

**Nota:** El archivo `requirements.txt` incluye las siguientes librerías:
- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `scipy`
- `statsmodels`
- `pmdarima`
- `scikit-learn`
- `joblib`
- `kagglehub`
- `jupyter`
- `tqdm`
- `session-info`

### 4. Ejecutar el notebook

Finalmente, lanza Jupyter Notebook para abrir el archivo principal:
```bash
jupyter notebook Madrid_Air_Pollution_Forecasting.ipynb 
```

### 5. (Opcional) Descargar el dataset

El notebook descargará automáticamente el dataset desde Kaggle usando `kagglehub`. Si es la primera vez, asegúrate de tener configuradas tus credenciales de Kaggle.

***

## 📈 Contenido del Análisis

### 1. Análisis Exploratorio de Datos (EDA)
- Carga y concatenación de archivos CSV anuales
- Agregación diaria (promedio entre estaciones)
- Visualización de series temporales (diarias, mensuales, anuales)

### 2. Análisis de Estacionariedad
- **Test ADF (Augmented Dickey-Fuller):** Hipótesis nula → serie no estacionaria
- **Test KPSS (Kwiatkowski-Phillips-Schmidt-Shin):** Hipótesis nula → serie estacionaria
- Interpretación combinada de ambos tests

### 3. Descomposición Estacional
- Modelo aditivo y multiplicativo
- Separación en componentes: Tendencia + Estacionalidad + Residuo

### 4. Transformaciones y Diferenciación
- **Box-Cox:** Estabilización de varianza
- **Diferenciación (orden 1):** Eliminación de tendencia

### 5. Modelos de Forecasting

| Modelo | Descripción | Parámetros |
|--------|-------------|------------|
| **ARIMA** | Autoregressive Integrated Moving Average | p, d, q (seleccionados automáticamente con auto_arima) |
| **SES** | Simple Exponential Smoothing | α (smoothing level) |
| **Holt** | Doble suavizado exponencial (con tendencia) | α, β |
| **Holt-Winters** | Triple suavizado exponencial (tendencia + estacionalidad) | α, β, γ, s |

### 6. Métricas de Evaluación
- **MSE (Mean Squared Error):** Penaliza errores grandes
- **RMSE (Root Mean Squared Error):** Error en unidades originales
- **MAE (Mean Absolute Error):** Robusto a outliers
- **MAPE (Mean Absolute Percentage Error):** Error relativo porcentual

***

## 📊 Resultados Principales

### Hallazgos Clave

| Contaminante | Tendencia | Estacionalidad | Mejor Modelo |
|--------------|-----------|----------------|--------------|
| **NO₂** | Descendente (políticas de control de emisiones) | Fuerte (mayor en invierno) | Holt-Winters |
| **CO** | Descendente pronunciado (mejora tecnológica) | Suave | Holt-Winters |

### Resultados de Estacionariedad

| Gas | ADF (p-value) | KPSS (p-value) | Conclusión |
|-----|---------------|----------------|------------|
| NO₂ | < 0.05 (estacionaria) | < 0.05 (no estacionaria) | Estacionaria en diferencia (tiene tendencia) |
| CO  | < 0.05 (estacionaria) | < 0.05 (no estacionaria) | Estacionaria en diferencia (tiene tendencia) |

### Resultados después de Box-Cox + Diferenciación

| Gas | λ Box-Cox | ADF (p-value) | KPSS (p-value) | Estado |
|-----|-----------|---------------|----------------|--------|
| NO₂ | 0.489 | < 0.0001 | > 0.05 | Estacionaria |
| CO  | -0.572 | < 0.0001 | > 0.05 | Estacionaria |

***

## 🗺️ Visualizaciones Incluidas

- Series temporales diarias de NO₂ y CO
- Promedios mensuales y anuales
- Descomposición estacional (aditiva y multiplicativa)
- Comparación antes/después de transformaciones
- Pronóstico ARIMA con intervalos de confianza
- Comparativa de modelos de suavizado exponencial
- Gráfico de barras de métricas de error

***

## 📚 Dependencias

| Categoría | Librerías |
|-----------|-----------|
| **Cálculo científico** | `numpy`, `pandas`, `scipy` |
| **Visualización** | `matplotlib`, `seaborn` |
| **Series temporales** | `statsmodels`, `pmdarima` |
| **Machine Learning** | `scikit-learn`, `joblib` |
| **Jupyter** | `jupyter`, `ipykernel`, `session-info` |
| **Utilidades** | `tqdm`, `kagglehub` |

***

## 📄 Licencia

Este proyecto está bajo la **Licencia MIT**. Consulta el archivo [LICENSE](LICENSE) para más detalles.

***

## 🙏 Agradecimientos

- **decide-soluciones** por publicar el dataset en Kaggle
- **Ayuntamiento de Madrid** por proporcionar los datos abiertos
- Comunidad open source por `statsmodels`, `pmdarima`, `scipy` y demás librerías

***

## 📚 Referencias

- Box, G. E. P., Jenkins, G. M., Reinsel, G. C., & Ljung, G. M. (2015). *Time Series Analysis: Forecasting and Control*. John Wiley & Sons.
- Hyndman, R. J., & Athanasopoulos, G. (2018). *Forecasting: Principles and Practice*. OTexts.
- [Statsmodels Documentation](https://www.statsmodels.org/)
- [pmdarima Documentation](https://alkaline-ml.com/pmdarima/)

***

## 👤 Autor

**Sebastián Deghi**
- GitHub: [@SebastianDeghi](https://github.com/SebastianDeghi)
- LinkedIn: [@sebastian-deghi](https://www.linkedin.com/in/sebastian-deghi/)
- Google Scholar: [@Sebastian E. Deghi](https://scholar.google.com/citations?user=3Nq5hTIAAAAJ&hl=en)