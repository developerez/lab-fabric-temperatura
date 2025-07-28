## 🚀 Pipeline Completo del Laboratorio

### 1️⃣ Notebook: `nb_create_table_anios`
- **Tipo:** Notebook (PySpark)
- **Objetivo:** Detectar automáticamente años disponibles desde GitHub del Ministerio de Ciencia de Chile.
- **Salida:** Tabla Delta `tabla_anios` con columna `anio`.
- **Técnicas:** PySpark, `input_file_name()`, regex.

### 2️⃣ Lookup: `array_annios`
- **Tipo:** Actividad de búsqueda
- **Objetivo:** Convertir la tabla `tabla_anios` en arreglo para iteración.
- **Salida:** Array de años: `[2020, 2021, 2022, 2023, ...]`
- **Consulta:** `SELECT anio FROM tabla_anios`

### 3️⃣ ForEach: `ciclo_copia`
- **Tipo:** Ciclo dinámico
- **Objetivo:** Ejecutar dinámicamente copiado de archivos CSV por año.
- **Parámetros:** `@activity('array_annios').output.value`

#### 🔄 Actividad interna: `copiar_ficheros_github`
- **Tipo:** Copy Data
- **Origen:** HTTP
  - **URL:** relativa, por año, e.g.: `/output/temperatura_dmc/{anio}/*.csv`
  - **Método HTTP:** GET
  - **Configuración conexión HTTP:** autenticación anónima
- **Destino:** Data Lake Microsoft Fabric
  - **Carpeta destino:** `/temperatura_dmc/{anio}`

### 4️⃣ Notebook: `nb_mover_csv`
- **Tipo:** Notebook (PySpark)
- **Objetivo:** Mover archivos CSV descargados por año a carpeta plana.
- **Origen:** `/temperatura_dmc/{anio}`
- **Destino:** `/temperatura_dmc_flat`

### 5️⃣ Notebook: `nb_crear_tabla_temp_dmc`
- **Tipo:** Notebook (PySpark)
- **Objetivo:** Crear tabla Delta enriquecida con columna `anio`.
- **Origen:** Carpeta plana `/temperatura_dmc_flat`
- **Destino:** Tabla Delta analítica `temperatura_dmc`

---

### 📌 Imagen asociada:
- **Archivo:** `images/pipeline_completo.png`

