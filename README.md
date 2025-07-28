# 🌡️ Laboratorio de ingestión y transformación de datos meteorológicos con Microsoft Fabric

Este laboratorio muestra cómo automatizar la carga, consolidación y transformación de archivos CSV de temperatura provenientes del repositorio GitHub del Ministerio de Ciencia de Chile, usando pipelines y notebooks en Microsoft Fabric.

---

## 🔗 Flujo general del pipeline (Fabric)

### 1️⃣ Actividad: Crear tabla de años

![Actividad crear tabla de años](images/actividad_tabla_annios.png)

- **Descripción:** Notebook que detecta los años disponibles en GitHub y actualiza la tabla Delta `tabla_annios` automáticamente.
- **Automatización total:** La tabla se crea si no existe y se actualiza con nuevos años sin intervención manual.

🔗 [Ver notebook nb_create_table_annios.ipynb](nb_create_table_annios.ipynb)

---

### 2️⃣ Actividad: Mover archivos a carpeta plana

![Actividad mover archivos](images/actividad_mover_csv.png)

- **Descripción:** Notebook que mueve todos los archivos `.csv` descargados de subcarpetas por año a una sola carpeta plana (`temperatura_dmc_flat`), facilitando la ingestión y el procesamiento.
- **Automatización total:** Se asegura de que todos los archivos estén listos para la etapa de consolidación.

🔗 [Ver notebook nb_mover_csv.ipynb](nb_mover_csv.ipynb)

---

### 3️⃣ Actividad: Crear y transformar tabla Delta

![Actividad crear tabla temperatura](images/actividad_tabla_temperatura.png)

- **Descripción:** Notebook Spark que:
  - Lee todos los archivos `.csv` desde la carpeta plana.
  - Guarda los datos en formato Delta.
  - Crea y registra automáticamente la tabla Delta externa `temperatura_dmc`.
  - Añade la columna `anio` extraída de la columna `time` usando Spark y habilita `mergeSchema` para evolución del esquema.
- **Automatización total:** La tabla se crea o actualiza sin pasos manuales, solo ejecutando el pipeline.

🔗 [Ver notebook nb_crear_tabla_temperatura.ipynb](nb_crear_tabla_temperatura.ipynb)

---

## ⚙️ Automatización y parámetros clave

- Todas las conexiones, rutas y nombres de archivos son **dinámicos** y se orquestan desde el pipeline.
- No hay pasos manuales: todo (carpetas, tablas, ingestión y transformación) se crea y actualiza automáticamente con los notebooks y actividades del pipeline.
- La tabla final es una **tabla Delta externa**.

---

## 📂 Archivos en este repositorio

- `nb_create_table_annios.ipynb`: Notebook para detectar años y crear tabla Delta.
- `nb_mover_csv.ipynb`: Notebook para mover archivos a un directorio plano.
- `nb_crear_tabla_temperatura.ipynb`: Notebook para crear y enriquecer la tabla Delta.
- `README.md`: Esta documentación.
- `/images/`: Carpeta con capturas de pantalla de las actividades.

---

## 🚀 Autor

Desarrollado por developerez  
Laboratorio de automatización de ingestión y transformación de datos meteorológicos usando Microsoft Fabric y GitHub.
