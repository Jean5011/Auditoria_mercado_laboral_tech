# 📊 Auditoría del Mercado Laboral Tecnológico (Data Jobs ETL & Relational EDA)

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![SQLite](https://img.shields.io/badge/SQLite-3-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://www.sqlite.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Status](https://img.shields.io/badge/Status-Finalizado-success?style=for-the-badge)](#)

Pipeline integral de ingeniería y análisis de datos (ETL & EDA) que transforma un conjunto de datos desestructurado y ruidoso de más de **2,250 ofertas laborales del sector tech** (Glassdoor/Kaggle) en una base de datos relacional estructurada, extrayendo métricas y KPIs clave de compensación y demanda laboral mediante **SQL**.

---

## 🎯 Objetivo del Proyecto

Construir un flujo de trabajo reproducible, modular y robusto que cubra el ciclo de vida completo de un Científico / Ingeniero de Datos:
1. **Ingesta y diagnóstico inicial** de anomalías e inconsistencias.
2. **Tratamiento avanzado y limpieza (Data Wrangling)** mediante expresiones regulares (Regex) y estrategias diferenciadas de imputación.
3. **Persistencia e integridad relacional** en un motor SQL estructurado.
4. **Análisis exploratorio de datos (EDA)** con consultas SQL aplicando rigor estadístico (control de significancia muestral $n \ge 30$).

---

## 🏗️ Arquitectura del Pipeline

```
[ Dataset Crudo: CSV (2,253 × 16) ]
                 │
                 ▼
┌─────────────────────────────────────────┐
│ FASE 1: Ingesta & Perfilado de Datos    │ ──► Diagnóstico de nulos ocultos y variables residuales
└─────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ FASE 2: Limpieza y Normalización (ETL)  │ ──► Regex para salarios, imputación robusta y tipado estricto
└─────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ FASE 3: Persistencia Relacional         │ ──► Modelado y carga en SQLite (`DataAnalyst.db`)
└─────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ FASE 4: Explotación Analítica (SQL EDA) │ ──► Agregaciones, métricas sectoriales, geográficas y de roles
└─────────────────────────────────────────┘
```

---

## 📈 Tablero de Métricas y Hallazgos Principales (KPIs)

* **Compensación Global:**
  * **Media Salarial de Mercado:** `$72,121.28 USD / año`
  * **Piso Salarial (Min):** `$33,500.00 USD` | **Techo Salarial (Max):** `$150,000.00 USD`
  * **Rango:** `$116,500.00 USD` (marcada dispersión según geografía y sector).

* **Sectores Más Rentables vs. Mayor Demanda ($n \ge 30$):**
  * 🏆 **Mejor Remunerado:** *Biotech & Pharmaceuticals* con **$83,106 USD** (+15.2% sobre la media).
  * 📊 **Mayor Demanda Laboral:** *Information Technology* (570 vacantes) y *Business Services* (523 vacantes).

* **Distribución Geográfica ($n \ge 30$):**
  * 🏆 **Silicon Valley:** *San Jose, CA* lidera con un promedio de **$108,855 USD** (+50.9% sobre la media global).
  * 🏙️ **Volumen:** *New York, NY* concentra el mayor volumen (310 vacantes) con salarios en la media ($71,235 USD).

---

## 🛠️ Tecnologías y Metodología

| Componente | Tecnología | Uso en el Proyecto |
|---|---|---|
| **Lenguaje** | Python 3.x | Lógica principal de ingesta, manipulación y tipado |
| **Manipulación** | Pandas & NumPy | Operaciones vectorizadas sobre DataFrames y transformaciones |
| **Parsing Textual** | Regex (`re`) | Extracción de rangos salariales `$XXK-$YYK` a variables numéricas |
| **Base de Datos** | SQLite3 | Almacenamiento persistente relacional y validación de esquemas |
| **Consultas** | SQL Estándar | Álgebra relacional (`GROUP BY`, `HAVING`, `AVG`, agregaciones) |
| **Entorno** | VS Code / Jupyter | Desarrollo modular documentado paso a paso |

---

## 📁 Estructura del Repositorio

```text
├── data/
│   ├── DataAnalyst.csv          # Dataset crudo original (2,253 registros)
│   └── DataAnalyst.db           # Base de datos SQLite normalizada y saneada (2,251 registros)
├── Documentacion/
│   ├── Planificacion/           # Planificación de fases y objetivos
│   ├── Documentacion_Fase1.md   # Diagnóstico y perfilado
│   ├── Documentacion_Fase2.md   # Data Wrangling y transformaciones
│   ├── Documentacion_Fase3.md   # Persistencia relacional
│   ├── Documentacion_Fase4.md   # Consultas analíticas
│   └── Reporte_Final_Cierre.md  # Reporte ejecutivo y cierre del proyecto
├── notebooks/
│   └── auditoria_mercado_laboral_tech.ipynb  # Pipeline ejecutable de punta a punta
└── README.md
```

---

## 🚀 Instalación y Uso

1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/tu-usuario/auditoria-mercado-laboral-tech.git
   cd auditoria-mercado-laboral-tech
   ```

2. **Crear y activar entorno virtual:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # En Windows: venv\Scripts\activate
   ```

3. **Instalar dependencias:**
   ```bash
   pip install pandas numpy jupyter
   ```

4. **Ejecutar el Notebook:**
   ```bash
   jupyter notebook notebooks/auditoria_mercado_laboral_tech.ipynb
   ```

---

## 👨‍💻 Autor

Desarrollado con foco en buenas prácticas de ingeniería de software, arquitectura de datos y modelado relacional.
