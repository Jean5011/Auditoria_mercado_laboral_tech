# Reporte Descriptivo Final — Auditoría del Mercado Laboral Tecnológico

> **Tipo de Documento:** Reporte de Cierre de Proyecto  
> **Fecha de Cierre:** 17 de Agosto, 2026  
> **Ciclo Completado:** 4 Fases (Ingesta → Limpieza → Persistencia → EDA)  
> **Estado:** ✅ Finalizado

---

## 1. Contexto del Proyecto

### 1.1 Descripción
Pipeline end-to-end de ciencia de datos sobre un dataset de **2,253 ofertas laborales** del sector tecnológico (fuente: Kaggle / Glassdoor). El proyecto simuló el proceso completo que ejecuta un Científico/Ingeniero de Datos: desde la ingesta de datos crudos hasta la extracción de insights accionables.

### 1.2 Objetivo Original
> *"Desarrollar un flujo de trabajo (pipeline) limpio y reproducible que transforme un dataset 'sucio' de vacantes de empleo en una base de datos relacional perfectamente estructurada."*
>
> — Planificación del Proyecto

### 1.3 Stack Tecnológico Utilizado

| Componente | Herramienta | Justificación |
|---|---|---|
| Entorno | Jupyter Notebook (VS Code) | Documentación intercalada con ejecución modular |
| Lenguaje | Python 3.x | Ecosistema dominante en ciencia de datos |
| Manipulación | Pandas + NumPy | Operaciones vectorizadas sobre DataFrames |
| Persistencia | SQLite3 | Motor relacional embebido, sin servidor |
| Consultas | SQL estándar | Álgebra relacional para análisis descriptivo |

---

## 2. Resumen Ejecutivo

El proyecto completó exitosamente las **4 fases planificadas**, transformando un dataset con severas inconsistencias (salarios como texto, valores centinela, índices residuales, escasez de datos) en una base de datos relacional limpia y consultable.

### Transformación del Dataset

```
ENTRADA                              SALIDA
─────────────────────                ─────────────────────
2,253 registros                      2,251 registros
16 columnas                          15 columnas
Salarios como texto                  3 variables numéricas (Min/Max/Avg)
~5,700 datos faltantes ocultos       0 valores nulos
Sin persistencia                     Base de datos SQLite (DataAnalyst.db)
```

---

## 3. Tablero de KPIs — Hallazgos Cuantitativos

### 3.1 KPI de Compensación Global

| Indicador | Valor | Interpretación |
|---|---|---|
| **Media Salarial Global** | **$72,121.28 USD** | Compensación promedio para roles Data Analyst en EE.UU. |
| **Salario Mínimo del Mercado** | $33,500.00 USD | Piso salarial (roles entry-level / mercados de bajo costo) |
| **Salario Máximo del Mercado** | $150,000.00 USD | Techo salarial (roles senior / mercados premium) |
| **Rango Salarial** | $116,500.00 USD | Alta dispersión: factores como ubicación y sector impactan significativamente |

---

### 3.2 KPIs de Segmentación Sectorial

> **Criterio de filtrado:** Solo sectores con n ≥ 30 ofertas (significancia muestral por Teorema del Límite Central)

| # | Sector | Salario Promedio (USD) | Volumen (n) | Clasificación |
|---|---|---|---|---|
| 1 | **Biotech & Pharmaceuticals** | $83,106.06 | 33 | 🏆 Mejor pago |
| 2 | Accounting & Legal | $75,220.93 | 43 | Alta compensación |
| 3 | **Information Technology** | $74,247.37 | **570** | 📊 Mayor volumen |
| 4 | Health Care | $72,807.95 | 151 | Sobre la media |
| 5 | **Business Services** | $72,273.42 | **523** | 📊 2do mayor volumen |
| 6 | Manufacturing | $72,075.00 | 40 | En la media |
| 7 | Insurance | $70,254.90 | 51 | Bajo la media |
| 8 | Education | $69,567.31 | 52 | Bajo la media |

**Insight clave:** Biotech & Pharmaceuticals paga un **15.2% más** que la media global, pero Information Technology absorbe **17× más demanda** laboral.

---

### 3.3 KPIs de Distribución Geográfica

> **Criterio de filtrado:** Solo ubicaciones con n ≥ 30 ofertas

| # | Ubicación | Salario Promedio (USD) | Volumen (n) | Clasificación |
|---|---|---|---|---|
| 1 | **San Jose, CA** | **$108,855.26** | 38 | 🏆 Mejor pago (Silicon Valley) |
| 2 | **San Francisco, CA** | $99,273.11 | 119 | Hub tecnológico premium |
| 3 | San Diego, CA | $91,459.68 | 62 | Ecosistema biotech |
| 4 | Chicago, IL | $78,726.92 | 130 | Hub del Midwest |
| 5 | Phoenix, AZ | $72,657.14 | 35 | En la media |
| 6 | Denver, CO | $71,776.60 | 47 | En la media |
| 7 | **New York, NY** | $71,235.48 | **310** | 📊 Mayor volumen |

**Insight clave:** San Jose (Silicon Valley) paga un **50.9% más** que la media global. New York lidera en volumen pero su compensación está en la media — efecto de saturación de oferta laboral.

---

### 3.4 KPIs de Concentración por Perfil

| # | Título del Puesto | Volumen | Salario Promedio (USD) |
|---|---|---|---|
| 1 | **Data Analyst** | **404** | $72,576.73 |
| 2 | Senior Data Analyst | 90 | $70,138.89 |
| 3 | Junior Data Analyst | 30 | $63,533.33 |
| 4 | Business Data Analyst | 28 | $75,607.14 |
| 5 | Sr. Data Analyst | 21 | $77,357.14 |
| 6 | Data Quality Analyst | 17 | $68,823.53 |
| 7 | Data Analyst Junior | 17 | $62,647.06 |
| 8 | Data Analyst II | 17 | $65,235.29 |
| 9 | Data Governance Analyst | 16 | $68,718.75 |
| 10 | Lead Data Analyst | 15 | $80,800.00 |

**Insight clave:** Se detectó **fragmentación léxica** — variantes del mismo perfil con nomenclaturas distintas (ej. "Senior Data Analyst" vs "Sr. Data Analyst", "Junior Data Analyst" vs "Data Analyst Junior"). Esto es un hallazgo de calidad de datos relevante para futuros proyectos de NLP o normalización textual.

---

## 4. Trazabilidad de Datos por Fase

### Fase 1 — Ingesta y Diagnóstico

| Operación | Detalle |
|---|---|
| Ingesta | `pd.read_csv('./data/DataAnalyst.csv')` → 2,253 × 16 |
| Diagnóstico | `df.info()` — Identificación de índice residual, tipos incorrectos, nulos ocultos |
| Purga | Eliminación de `Unnamed: 0` (artefacto de scraping) |
| Subsetting | Aislamiento de variables anómalas (`Salary Estimate`, `Founded`, `Rating`) |

---

### Fase 2 — Limpieza y Normalización

| Operación | Técnica | Resultado |
|---|---|---|
| Extracción salarial | Regex `.str.extract(r'\$(\d+)K-\$(\d+)K')` | `Min_Salary`, `Max_Salary` |
| Conversión de tipos | `.astype(float) * 1000` | De texto a float64 con escala real |
| Feature Engineering | `(Max + Min) / 2` | `Avg_Salary` — variable objetivo |
| Saneamiento textual | `.str.split('\n')` | `Company Name` sin artefactos |
| Estandarización | `.replace([-1, '-1', 'Unknown'], NaN)` | Valores centinela → NaN nativo |
| Reducción dimensional | `.drop(['Easy Apply', 'Competitors'])` | Eliminación de variables irrecuperables (>76% nulos) |
| Imputación categórica | `.fillna('No Especificado')` | 7 variables categóricas tratadas |
| Imputación estadística | `.fillna(mediana)` | `Rating` imputado con centroide robusto |
| Listwise Deletion | `.dropna()` + `.reset_index()` | Purga final: 2,253 → 2,251 registros |

---

### Fase 3 — Persistencia Relacional

| Operación | Detalle |
|---|---|
| Conexión | `sqlite3.connect('./data/DataAnalyst.db')` |
| Migración | `.to_sql('ofertas_laborales', if_exists='replace', index=False)` |
| Auditoría | `SELECT COUNT(*) FROM ofertas_laborales` → **2,251 registros verificados** |
| Cierre | `conexion.close()` — Consolidación del archivo físico |

---

### Fase 4 — Análisis Exploratorio (EDA Relacional)

| Consulta | Técnica SQL | Hallazgo Principal |
|---|---|---|
| Tendencia central | `AVG`, `MIN`, `MAX` | Media global: $72,121 USD |
| Segmentación sectorial | `GROUP BY Sector HAVING n≥30` | Biotech lidera ($83,106) |
| Distribución geográfica | `GROUP BY Location HAVING n≥30` | San Jose, CA lidera ($108,855) |
| Concentración por perfil | `GROUP BY "Job Title" ORDER BY COUNT DESC` | "Data Analyst" domina (404 ofertas) |

---

## 5. Competencias Técnicas Demostradas

| Competencia | Herramienta / Técnica | Fase |
|---|---|---|
| Ingesta de datos | `pandas.read_csv()` | F1 |
| Perfilado y diagnóstico | `df.info()`, `df.isna()`, subsetting | F1 |
| Expresiones regulares | `.str.extract(regex)` — parsing vectorial | F2 |
| Type Casting | `.astype(float)` — conversión tipológica | F2 |
| Feature Engineering | Derivación de variables calculadas | F2 |
| Tratamiento de nulos | `fillna()`, `dropna()`, `replace()` — estrategias diferenciadas | F2 |
| Operaciones sobre ejes | `axis=0` (filas) vs `axis=1` (columnas) | F1, F2 |
| Persistencia relacional | `sqlite3` + `.to_sql()` | F3 |
| Auditoría de integridad | `SELECT COUNT(*)` — validación post-migración | F3 |
| Álgebra relacional | `SELECT`, `GROUP BY`, `HAVING`, `ORDER BY`, funciones de agregación | F4 |
| Pensamiento analítico | Control de significancia muestral (n ≥ 30) | F4 |

---

## 6. Registro de Artefactos Generados

### Código

| Artefacto | Ubicación |
|---|---|
| Notebook principal | `proyecto_auditoria_empleo/auditoria_mercado_laboral_tech.ipynb` |

### Datos

| Artefacto | Descripción |
|---|---|
| `data/DataAnalyst.csv` | Dataset crudo original (2,253 × 16) |
| `data/DataAnalyst.db` | Base de datos SQLite con tabla `ofertas_laborales` (2,251 × 15) |

### Documentación

| Artefacto | Fase |
|---|---|
| `Documentacion/Planificacion/Planificacion_Auditoria_Empleo_Tech.md` | Planificación |
| `Documentacion/Documentacion_Fase1.md` | Fase 1 |
| `Documentacion/Documentacion_Fase2.md` | Fase 2 |
| `Documentacion/Documentacion_Fase3.md` | Fase 3 |
| `Documentacion/Documentacion_Fase4_Finalizada.md` | Fase 4 |
| `Documentacion/Reporte_Final_Cierre.md` | **Este documento** |

---

## 7. Acta de Cierre

```
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║   PROYECTO: Auditoría del Mercado Laboral Tecnológico                ║
║   ESTADO:   ✅ FINALIZADO                                            ║
║                                                                      ║
║   Fases Completadas:                                                 ║
║     ✅ Fase 1 — Ingesta y Diagnóstico                                ║
║     ✅ Fase 2 — Limpieza y Normalización (Data Wrangling)            ║
║     ✅ Fase 3 — Persistencia Relacional (SQLite)                     ║
║     ✅ Fase 4 — Análisis Exploratorio de Datos (EDA Relacional)      ║
║                                                                      ║
║   Entregables Verificados:                                           ║
║     ✅ DataFrame limpio (0 nulos, tipos correctos)                   ║
║     ✅ Base de datos SQLite persistida (2,251 registros)             ║
║     ✅ KPIs extraídos mediante consultas SQL                         ║
║     ✅ Documentación completa por fase                               ║
║     ✅ Reporte descriptivo final                                     ║
║                                                                      ║
║   Fecha de Cierre: 17 de Agosto, 2026                                ║
║                                                                      ║
╚══════════════════════════════════════════════════════════════════════╝
```

---

> *El ciclo de cuatro fases ha sido completado satisfactoriamente. Todos los objetivos definidos en la planificación original fueron alcanzados.*
