# Planificación del Proyecto: Auditoría del Mercado Laboral Tecnológico

## 1. Perfil del Científico de Datos
* **Nivel Actual:** Inicial / Transición orientada a la práctica.
* **Fundamentos Consolidados:** Lógica algorítmica estructurada, experiencia en desarrollo de arquitecturas backend (servidores) y dominio de lenguajes fuertemente tipados.
* **Habilidades Objetivo:** Dominio de Python, SQL y limpieza profunda de datos (ETL/Data Wrangling).
* **Metodología de Trabajo:** Bloques de estudio enfocados de 30 minutos diarios, priorizando el desarrollo modular y la comprensión analítica.

---

## 2. Descripción del Proyecto
Este proyecto consiste en el diseño e implementación de un pipeline de procesamiento y análisis descriptivo sobre un conjunto de datos (dataset) de ofertas de empleo en el sector tecnológico, comúnmente extraído de plataformas como Kaggle. 

El núcleo del proyecto radica en enfrentarse a datos del "mundo real", los cuales típicamente presentan severas inconsistencias: formatos de salario mixtos o ausentes, descripciones de tecnologías desordenadas, valores nulos y registros duplicados. A través de este escenario, se simulará el proceso de ingesta, saneamiento y estructuración que realiza un Ingeniero/Científico de Datos antes de alimentar cualquier reporte de negocio o modelo predictivo.

---

## 3. Objetivo del Proyecto
Desarrollar un flujo de trabajo (pipeline) limpio y reproducible que transforme un dataset "sucio" de vacantes de empleo en una base de datos relacional perfectamente estructurada. 

**Metas Analíticas Específicas:**
* Normalizar y unificar los títulos de los puestos de trabajo.
* Extraer y estandarizar valores salariales mediante expresiones regulares (Regex).
* Catalogar e indexar las tecnologías requeridas más demandadas.
* Generar un reporte descriptivo final con KPIs mediante consultas SQL relacionales.

---

## 4. Stack Tecnológico y Justificación

Para garantizar la eficiencia y evitar la sobreingeniería, se ha seleccionado un stack tecnológico minimalista, donde cada herramienta se alinea con tus objetivos de aprendizaje y aprovecha tus fortalezas en backend:

* **Entorno de Desarrollo y Registro:** *Jupyter Notebooks* (ejecutado en VS Code local o Google Colab). Permite la intercalación de documentación explicativa (Markdown) y bloques de ejecución modular (Code), ideal para tus sesiones de 30 minutos.
* **Lenguaje Base:** *Python 3.x*. Utilizado por su dominio en el ecosistema de datos y su soporte para programación orientada a objetos (POO), lo que te permitirá encapsular lógica de limpieza compleja si fuera necesario.
* **Motor de Manipulación de Datos:** *Pandas*. Es la librería estándar de la industria. Su uso está plenamente justificado por su eficiencia en operaciones vectorizadas sobre memoria a través de sus dos estructuras clave: `Series` y `DataFrames`.
* **Motor de Almacenamiento y SQL:** *SQLite* (a través de la biblioteca nativa `sqlite3` de Python). Evita la necesidad de configurar servidores locales complejos de bases de datos. Almacena la información en un único archivo físico en disco, permitiéndote practicar SQL relacional nativo y asegurar que los datos limpios cumplan con restricciones de integridad de esquemas.

---

## 5. Análisis Arquitectónico del Proyecto

El ciclo de vida del proyecto se dividirá de forma estricta en cuatro fases modulares. Cada fase representará metas específicas para tus bloques diarios de estudio:

```
[ Dataset Crudo (CSV) ]
           │
           ▼
[ FASE 1: Ingesta y Diagnóstico ] ────────► Análisis de tipos, nulos y anomalías.
           │
           ▼
[ FASE 2: Limpieza y Normalización ] ─────► Uso de Regex, imputación y tipado estricto.
           │
           ▼
[ FASE 3: Persistencia Relacional ] ──────► Mapeo a Esquema SQLite.
           │
           ▼
[ FASE 4: Explotación Analítica ] ────────► Consultas SQL y obtención de KPIs.
```

### Fase 1: Ingesta y Diagnóstico (Perfilado de Datos)
* **Objetivo:** Cargar el archivo origen (CSV) e inspeccionar su estructura interna.
* **Operaciones Clave:** * Uso de `.read_csv()` con parámetros de codificación correctos.
    * Inspección de metadatos mediante `.info()`, `.describe()` y `.shape`.
    * Identificación y cuantificación de valores ausentes (`.isnull().sum()`).
* **Entregable de Fase:** Un diagnóstico inicial documentado en el cuaderno identificando las columnas críticas a corregir.

### Fase 2: Limpieza y Normalización (Data Wrangling)
* **Objetivo:** Corregir los errores estructurales y de contenido detectados en la Fase 1.
* **Operaciones Clave:**
    * *Normalización de Texto:* Convertir títulos a minúsculas/mayúsculas estándar y eliminar espacios en blanco innecesarios (`.str.strip()`, `.str.lower()`).
    * *Extracción de Salarios:* Uso de expresiones regulares (`.str.extract()`) para aislar números de caracteres como "$", "USD", o rangos ("80k-100k") y convertirlos a flotantes/enteros.
    * *Tratamiento de Nulos:* Decidir estratégicamente si eliminar filas o rellenar valores ausentes (imputación con la mediana o marcas de "No Especificado") usando `.fillna()` o `.dropna()`.
* **Entregable de Fase:** Un DataFrame de Pandas completamente limpio, con tipos de datos correctos y homogéneos.

### Fase 3: Persistencia Relacional (Diseño de Base de Datos)
* **Objetivo:** Migrar los datos en memoria hacia un almacenamiento persistente bajo un esquema relacional básico.
* **Operaciones Clave:**
    * Establecer conexión con SQLite mediante `sqlite3.connect()`.
    * Definición explícita de un esquema de tabla (tipos de datos SQL como `INTEGER`, `TEXT`, `REAL`).
    * Volcado de datos desde Pandas usando `.to_sql()` aplicando restricciones de reemplazo o adición (`if_exists='replace'`).
* **Entregable de Fase:** Un archivo de base de datos `.db` local con la tabla de empleo estructurada y optimizada.

### Fase 4: Explotación Analítica (Análisis Descriptivo)
* **Objetivo:** Responder a las preguntas de negocio utilizando el lenguaje SQL estándar sobre la base de datos creada.
* **Operaciones Clave:**
    * Escritura de consultas con cláusulas `SELECT`, `WHERE`, `GROUP BY`, `ORDER BY` y funciones de agregación (`AVG`, `COUNT`, `MAX`).
    * Extracción de métricas clave (ej. Salario promedio por lenguaje de programación, roles con mayor volumen de ofertas, distribución geográfica de vacantes).
* **Entregable de Fase:** Conjunto de consultas SQL ejecutadas dentro del cuaderno que devuelven las respuestas estructuradas a los objetivos del proyecto.
