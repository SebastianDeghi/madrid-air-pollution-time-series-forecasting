Análisis de series temporales de contaminantes atmosféricos en Seúl

# 🌍 Análisis de series temporales de contaminantes atmosféricos en Seúl

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-notebook-orange)](https://jupyter.org/)
[![Geopandas](https://img.shields.io/badge/geopandas-mapping-green)](https://geopandas.org/)
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

## 📊 Descripción del Dataset

- **Fuente:** Datos horarios de calidad del aire de Madrid (2001-2018)
- **Contaminantes:** NO₂ (Dióxido de Nitrógeno) y CO (Monóxido de Carbono)
- **Estructura:** Archivos CSV anuales (`madrid_2001.csv` a `madrid_2018.csv`)
- **Procesamiento:** Agregación diaria (promedio entre estaciones)

---

## 🔧 Instalación y Uso

### 1. Clonar el repositorio

```bash
git clone https://github.com/SebastianDeghi/madrid-air-pollution-time-series-forecasting.git
cd madrid-air-pollution-time-series-forecasting

***

## 🚀 Contaminantes Analizados

| Contaminante | Fuente Principal | Unidad | Umbral "Bad" (malo) |
| :--- | :--- | :--- | :--- |
| **PM10** | Polvo, construcción, tráfico | µg/m³ | 150 |
| **PM2.5** | Combustión, industria | µg/m³ | 75 |
| **SO2** | Industria, calefacción | ppm | 0.15 |
| **NO2** | Tráfico vehicular | ppm | 0.20 |
| **O3** | Formación fotoquímica | ppm | 0.15 |
| **CO** | Combustión incompleta | ppm | 15 |

**Conclusión Clave:** El NO₂ muestra un patrón diario claro asociado al tráfico (picos en horas pico 8-9 AM y 6-7 PM). Las estaciones cercanas a autopistas presentan valores ~20-30% más altos. O₃ presenta anticorrelación con NO₂ (formación fotoquímica en horas de mayor radiación solar). PM10 y PM2.5 muestran episodios agudos asociados a tormentas de polvo asiático y estancamiento atmosférico.

***

## 🗺️ Visualizaciones Implementadas

- **Mapa satelital** con las 25 estaciones de monitoreo geolocalizadas
- **Gráficos de barras** de umbrales de calidad del aire (Good, Normal, Bad, Very Bad)
- **Series temporales** por estación y contaminante (antes y después de limpieza)
- **Patrones horarios de NO₂** con marcado de horas pico de tráfico
- **Análisis espectral** (periodograma) para detectar ciclos diarios en NO₂
- **Comparación** de estaciones cerca vs lejos de autopistas

***

## 🔧 Instalación y Uso

Sigue estos pasos para clonar el repositorio, configurar el entorno y ejecutar el análisis en tu máquina local.

### 1. Clonar el repositorio

Abre tu terminal y ejecuta:
```bash
git clone https://github.com/SebastianDeghi/seoul-air-pollution-time-series-analysis.git
cd seoul-air-pollution-time-series-analysis
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
- `geopandas`
- `contextily`
- `scipy`
- `statsmodels`
- `kagglehub`
- `jupyter`
- `tqdm`
- `session-info`

## 📈 Hallazgos Principales

| Contaminante | Hallazgo Clave |
|--------------|----------------|
| **PM10 y PM2.5** | Picos agudos (>150 µg/m³) por eventos de polvo asiático; las estaciones urbanas muestran promedios más altos |
| **NO2** | Patrón diario de tráfico claro (picos a las 8-9 AM y 6-7 PM); estaciones cerca de autopistas muestran valores ~20-30% más altos |
| **O3** | Anticorrelación con NO2 (formación fotoquímica); máximo durante el mediodía en verano |
| **SO2 y CO** | Generalmente bajos debido a políticas ambientales exitosas; pequeños picos en invierno por calefacción |

### Problemas de Calidad de Datos Detectados y Corregidos

- Picos idénticos extremadamente altos en PM10/PM2.5 (saturación de sensores >950 µg/m³) → reemplazados por NaN
- Valores negativos en SO2 (errores instrumentales) → reemplazados por NaN

---

## 🗺️ Visualizaciones Incluidas

- Mapa satelital con las 25 estaciones de monitoreo
- Gráficos de series temporales por estación y contaminante
- Gráficos de barras de umbrales de calidad del aire (Bueno, Normal, Malo, Muy Malo)
- Patrones horarios de NO2 con marcado de horas pico de tráfico
- Análisis espectral (periodograma) para ciclos diarios de NO2
- Comparación de estaciones cerca vs. lejos de autopistas

---

## 📚 Dependencias

- `numpy`, `pandas`, `matplotlib`, `seaborn`
- `geopandas`, `contextily`, `shapely` (para mapas)
- `scipy`, `statsmodels` (para análisis espectral y series temporales)
- `kagglehub` (para descarga del dataset)
- `jupyter`, `session-info`

---

## 📄 Licencia

Este proyecto está bajo la **Licencia MIT**. Consulta el archivo [LICENSE](LICENSE) para más detalles.

---

## 🙏 Agradecimientos

- **Bappekim** por publicar el dataset en Kaggle
- **Gobierno Metropolitano de Seúl** por proporcionar los datos abiertos
- **Seoul Open Data Plaza** y **Air Quality Analysis Center**

---

## 👤 Autor

**Sebastián Deghi**

- GitHub: [@SebastianDeghi](https://github.com/SebastianDeghi)
- LinkedIn: [@sebastian-deghi](https://www.linkedin.com/in/sebastian-deghi/)
- Google Scholar: [@Sebastian E. Deghi](https://scholar.google.com/citations?user=3Nq5hTIAAAAJ&hl=en)