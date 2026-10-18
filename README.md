# 📱 Análisis del Comportamiento de Clientes - ConnectaTel
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TU_USUARIO_GITHUB/project_ConectaTel/blob/main/project_ConectaTel.ipynb)
![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458.svg)
![Status](https://img.shields.io/badge/Estado-Finalizado-success.svg)

# 📌 Objetivo del Proyecto
Evaluar el comportamiento de consumo (llamadas y mensajes) y el perfil demográfico de los clientes de **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica, con datos registrados hasta el cierre de **2024**. 

El propósito del análisis es limpiar e integrar las fuentes de datos, construir un perfil estadístico por usuario, detectar valores atípicos (*outliers*) y segmentar la cartera de clientes para **identificar oportunidades comerciales, diseñar estrategias de retención y proponer mejoras en la oferta de planes**.

---
## 📂 Datasets Utilizados
El análisis integra tres fuentes de datos principales ubicadas en el directorio `/datasets/`:

1. **`plans.csv` (2 filas, 8 columnas):** Catálogo de planes actuales (`Basico` de $12 USD y `Premium` de $25 USD), detallando minutos, mensajes y GB incluidos, así como las tarifas por excedente.
2. **`users_latam.csv` (4,000 filas, 8 columnas):** Información demográfica y contractual de los clientes (`user_id`, nombre, apellido, `age`, `city`, `reg_date`, `plan` y `churn_date`).
3. **`usage.csv` (40,000 filas, 6 columnas):** Registro histórico detallado de eventos de uso del servicio (`id`, `user_id`, `type` [`call` / `text`], `date`, `duration` en minutos y `length` en caracteres).

---
## 🛠️ Etapas del Análisis Realizadas

1. **Carga y Exploración Inicial (Paso 1):** Inspección de dimensiones (`.shape`), tipos de datos (`.info()`) y vista preliminar de registros.
2. **Diagnóstico de Calidad de Datos (Paso 2):**
   - Evaluación de valores nulos y distinción entre errores de captura y nulos con significado de negocio (`churn_date` con 88.35% de clientes activos) o estructurales (`duration` con 55.19% y `length` con 44.74%).
   - Detección de valores centinela: edades negativas (`-999` en `age`), caracteres inválidos (`'?'` en `city`) y fechas de registro futuras (`2026-05-10` en `reg_date`).
3. **Limpieza y Transformación de Datos (Paso 3):**
   - Imputación de centinelas en `age` con la mediana (47 años), estandarización de `'?'` a `<NA>` en `city` y conversión de fechas futuras a `NaT`.
   - Comprobación estadística de nulos **MAR (*Missing At Random*)** en `duration` y `length` condicionados por `type`.
4. **Agregación y Perfil Estadístico por Usuario (Paso 4):**
   - Filtrado de eventos válidos del año 2024 y agrupación por `user_id` para obtener `cant_mensajes`, `cant_llamadas` y `cant_minutos_llamada`.
   - Integración (`merge`) con el padrón de usuarios (`user_profile` con 3,999 clientes activos) y análisis de distribución por plan (64.87% Básico vs. 35.13% Premium).
5. **Visualización de Distribuciones y Detección de *Outliers* (Paso 5):**
   - Generación de histogramas segmentados por plan y diagramas de caja (*boxplots*).
   - Cálculo de límites mediante el rango intercuartílico (**método IQR**) y decisión estratégica de conservar los *outliers* superiores al representar clientes reales de alto consumo.
6. **Segmentación de Clientes (Paso 6):**
   - Clasificación conductual en `grupo_uso` (**Bajo uso**, **Uso medio**, **Alto uso**).
   - Clasificación demográfica en `grupo_edad` (**Joven**, **Adulto**, **Adulto Mayor**).
7. **Insights Ejecutivos y Recomendaciones (Paso 7):** Traducción de hallazgos en propuestas de *upselling*, retención, rediseño de planes y mejora en la captura de datos.

---

## 🚀 Cómo Ejecutar el Notebook y Guía de Reproducción

### Requisitos Previos
El proyecto fue desarrollado en **Python 3** utilizando las siguientes librerías estándar de Ciencia de Datos:
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`

## 📂 Estructura del Repositorio
```text
📦 project_ConectaTel
 ┣ 📂 datasets
 ┃ ┣ 📜 plans.csv          # Especificaciones y costos de los planes tarifarios
 ┃ ┣ 📜 usage.csv          # Registro histórico de consumo de los usuarios
 ┃ ┗ 📜 users_latam.csv    # Información demográfica y estado de suscripción
 ┣ 📜 project_ConectaTel.ipynb  # Notebook con el desarrollo completo del proyecto
 ┗ 📜 README.md                 # Documentación ejecutiva del proyecto

Cómo ejecutar este proyecto
En la nube (1 clic): Haz clic en el botón Open in Colab en la parte superior de este documento para ejecutar el notebook directamente en el navegador (los datos se cargan automáticamente desde este repositorio).

En entorno local:

Bash
git clone [https://github.com/fercho9586/Project_ConectaTel.git](https://github.com/fercho9586/project_ConectaTel.git)
cd project_ConectaTel
jupyter notebook project_ConectaTel.ipynb
✒️ Autor: Analytics Engineer José Fernando Contreras Guerrero

🔗 [Tu enlace a LinkedIn]
