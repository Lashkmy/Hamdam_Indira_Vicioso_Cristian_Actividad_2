# 🚀 Actividad 2: Infraestructura y Procesamiento de Datos con Spark

![Databricks](https://img.shields.io/badge/Databricks-Runtime%2012.2%20LTS-FF3621?style=for-the-badge&logo=databricks)
![Spark](https://img.shields.io/badge/Apache%20Spark-3.3.2-E25A1C?style=for-the-badge&logo=apachespark)
![Python](https://img.shields.io/badge/Python-3.9-3776AB?style=for-the-badge&logo=python)

Este repositorio contiene la solución completa para la **Actividad 2**, enfocada en la configuración de un entorno de Big Data, el diseño de esquemas robustos y la validación de datos masivos utilizando **PySpark** y **Spark SQL** en Databricks Community Edition.

## 👥 Autores
* **Indira Hamdam**
* **Cristian Vicioso**

---

## 📋 Descripción del Proyecto

El objetivo principal es desplegar un pipeline de ingeniería de datos que ingeste, transforme y valide un dataset de calidad del aire proveniente de dispositivos IoT multisensor. El proyecto abarca desde la infraestructura hasta el análisis comparativo de paradigmas de programación (Imperativo vs. Declarativo).

### 📂 Estructura del Repositorio
| Archivo | Descripción |
| :--- | :--- |
| `Actividad2_Notebook.dbc` | **Código Fuente.** Archivo nativo de Databricks (incluye código, gráficas y salidas). |
| `Actividad2_Export.html` | **Reporte Visual.** Versión HTML estática para visualización rápida sin entorno Spark. |
| `README.md` | Documentación técnica y metodología del proyecto. |

---

## 🛠️ Infraestructura y Configuración

El proyecto fue ejecutado en **Databricks Community Edition** bajo la siguiente configuración:

* **Cluster Mode:** Single Node (Driver + Executor compartidos).
* **Databricks Runtime:** 12.2 LTS (Scala 2.12, Spark 3.3.2).
* **Instancia:** AWS Free Tier (6 GB Memory, 0.88 Cores).
* **Almacenamiento:** DBFS (Databricks File System) para la persistencia de archivos planos y Tablas Delta.

---

## 📊 Datos y Diseño del Esquema

**Fuente:** [Air Quality Data Set (UCI Machine Learning Repository / Kaggle)](https://www.kaggle.com/datasets/fedesoriano/air-quality-data-set)  
**Descripción:** Serie temporal con 9357 registros de respuestas horarias de sensores químicos (PT08.S1-S5).

### Modelo de Datos (Entidad-Relación)
Se diseñó un esquema normalizado para optimizar el almacenamiento columnar. Los campos numéricos se tiparon como `Double` para permitir agregaciones, y se manejó la nulabilidad (`Nullable=True`) debido a la naturaleza inestable de los sensores IoT.

```mermaid
erDiagram
    AIR_QUALITY {
        date Date PK "Fecha de lectura"
        time String PK "Hora de lectura"
        double co_gt "CO (Real)"
        double pt08_s1_co "Sensor Tin Oxide"
        double nmhc_gt "Hidrocarburos"
        double c6h6_gt "Benceno"
        double nox_gt "Óxidos Nitrógeno"
        double temperature "Temperatura Amb."
        double rel_humidity "Humedad Relativa"
    }
