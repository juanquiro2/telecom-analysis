# telecom-analysis
Analisis exploratorio de datos para una empresa telefonica para identificar los segmentos donde fucionan mejor los planes de telefono.

# Análisis de Clientes y Uso de Servicios - ConnectaTel (Latam)

## 🎯 1. Objetivo del Proyecto
Evaluar el comportamiento comercial de los clientes de ConnectaTel (empresa de telecomunicaciones en Latinoamérica) con información registrada hasta el año 2024. El propósito principal es explorar, limpiar y analizar los datos para:
- Construir un perfil estadístico de la base de clientes.
- Detectar valores atípicos (outliers) y problemas de calidad de datos.
- Identificar patrones de consumo (llamadas y mensajes de texto) y su relación con los planes contratados (Básico vs. Premium).
- Sentar las bases para el diseño de estrategias de retención (análisis de churn) y optimización de planes.

## 📂 2. Datasets Utilizados
El análisis procesa e integra tres fuentes de datos principales en formato CSV:
- plans.csv: Información general de los planes tarifarios actuales de la compañía (precio mensual en USD, minutos incluidos, GB por mes, costo por excedentes de GB, mensajes y minutos).
- users_latam.csv: Datos demográficos y contractuales de los usuarios (ID de usuario, nombre, apellido, edad, ciudad, fecha de registro, plan contratado y fecha de cancelación/churn).
- usage.csv: Detalle transaccional del uso real de los servicios por parte de los clientes durante el año 2024 (tipo de servicio: llamada o texto, fecha, duración de llamadas en minutos y longitud de mensajes).  

## 🔍 3. Etapas del Análisis Realizadas
El desarrollo del proyecto dentro del Jupyter Notebook se divide en 5 etapas secuenciales:
- Paso 1: Carga y Exploración Inicial
  - Importación de librerías esenciales (pandas, numpy, matplotlib.pyplot, seaborn).   
  - Carga de los tres datasets en memoria (plans, users, usage) y revisión preliminar de su estructura mediante .head() y .shape.   
- Paso 2: Identificación de Problemas de Calidad de Datos
  - Conteo y cálculo de proporciones de valores nulos por columna (detección de nulos en city, churn_date, date, duration y length).
  - Búsqueda de valores inválidos o sentinels (como edades con el valor erróneo -999 y registros de uso con ceros).
  - Validación y estandarización de fechas para filtrar anomalías (ej. registros con años futuros erróneos como 2026).   
- Paso 3: Limpieza Básica de Datos
  - Reemplazo de sentinels en variables numéricas (imputación de la edad -999 por la mediana) y tratamiento de ciudades faltantes ("?" a NA).
  - Verificación de la naturaleza de los nulos en uso (duration vs length) comprobando que sigan un patrón MAR (Missing At Random), donde la ausencia de un campo depende estrictamente del tipo de servicio (call o text).  
- Paso 4: Resumen Estadístico y Agregación por Usuario
  - Agregación de la tabla transaccional usage a nivel de usuario (user_id) para calcular métricas clave: cantidad total de mensajes, cantidad de llamadas y minutos acumulados de llamadas en 2024.
  - Combinación de los datos agregados con el perfil de usuarios (users).
  - Obtención de estadísticos descriptivos (media, mediana, desviación estándar, mínimos y máximos) y distribución porcentual de los planes.  
- Paso 5: Visualización de Distribuciones y Detección de Outliers
  - Creación de histogramas comparativos segmentados por tipo de plan (hue='plan') para analizar la distribución de la edad, cantidad de mensajes, llamadas y minutos de llamada.
  -  Generación automatizada de diagramas de caja (boxplots) para la detección visual de valores atípicos. 

## ☁️ 4. Cómo Ejecutar el Notebook
Puedes ejecutar y probar este proyecto interactivo directamente en la nube mediante Google Colab sin necesidad de instalar dependencias locales:
- Haz clic en el botón o enlace para abrir el notebook en Google Colab (asegúrate de tener una cuenta de Google activa).
- Verifica que el entorno de ejecución disponga de Python y las librerías estándar de ciencia de datos (pandas, numpy, matplotlib, seaborn). Si no están preinstaladas, puedes añadirlas ejecutando en una celda:
Python!pip install pandas numpy matplotlib seaborn
- Asegúrate de estructurar la ruta de tus archivos CSV en el directorio del entorno tal como lo requiere el código (/datasets/plans.csv, /datasets/users_latam.csv, /datasets/usage.csv).   

## 🚀 5. Breve Guía de Reproducción
Para reproducir localmente este análisis en tu equipo, sigue estos pasos:
1. Clona o descarga este repositorio en tu máquina local.
2. Configura la estructura de carpetas: Crea una carpeta llamada datasets en el directorio raíz del proyecto y coloca dentro los tres archivos fuente provistos (plans.csv, users_latam.csv, usage.csv).
3. Crea un entorno virtual (recomendado) e instala las dependencias necesarias:

python -m venv venv
source venv/bin/activate  # En Windows usa: venv\Scripts\activate
pip install pandas numpy matplotlib seaborn jupyter

4. Inicia Jupyter Notebook:

   Bashjupyter notebook
   
5. Abre el archivo del notebook correspondiente y ejecuta las celdas secuencialmente de arriba hacia abajo (Shift + Enter) para replicar la limpieza, las agregaciones estadísticas y las gráficas generadas.   
