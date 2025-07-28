# \# 🌡️ Laboratorio de ingestión y transformación de datos meteorológicos con Microsoft Fabric

# 

# Este laboratorio muestra cómo automatizar la carga y transformación de archivos CSV de temperatura, provenientes del repositorio GitHub del Ministerio de Ciencia de Chile, usando pipelines y notebooks en Microsoft Fabric.

# 

# ---

# 

# \## 📁 Estructura del repositorio

# 

# \- `01\_detectar\_annios.ipynb` — Notebook que detecta y actualiza la lista de años disponibles en GitHub.

# \- `02\_mover\_csv\_a\_plano.ipynb` — Notebook que mueve los CSV de subcarpetas a una sola carpeta plana.

# \- `03\_crear\_tabla\_delta.ipynb` — Notebook que crea y transforma la tabla Delta final (`temperatura\_dmc`).

# \- `README.md` — Documentación y explicación del flujo.

# 

# ---

# 

# \## 🔗 Flujo resumido del pipeline

# 

# 1\. \*\*Detección de años\*\*  

# &nbsp;  Se consulta el API de GitHub y se actualiza la tabla `tabla\_annios` con los años nuevos.

# 

# 2\. \*\*Descarga y organización de archivos\*\*  

# &nbsp;  Se descargan los archivos `.csv` por año desde GitHub a Files en Fabric, cada uno en su subcarpeta de año.

# 

# 3\. \*\*Normalización de archivos\*\*  

# &nbsp;  Un notebook mueve todos los `.csv` a un directorio plano (`Files/temperatura\_dmc\_flat`).

# 

# 4\. \*\*Creación y transformación de tabla\*\*  

# &nbsp;  Un notebook lee todos los archivos desde la carpeta plana, crea la tabla Delta `temperatura\_dmc` y agrega la columna `anio` extraída del campo `time`.

# 

# ---

# 

# \## 🛠️ Notas de uso

# 

# \- El pipeline es \*\*reproducible y escalable\*\*: solo hay que añadir nuevos archivos al repositorio y ejecutar el flujo.

# \- Los notebooks están listos para ser ejecutados en Microsoft Fabric.

# \- Se recomienda crear la tabla desde la carpeta plana para evitar problemas de subcarpetas.

# 

# ---

# 

# \## 🚀 Autor

# 

# Desarrollado por \[Tu Nombre o tu usuario GitHub]  

# Repositorio de práctica con datos meteorológicos abiertos de Chile.

# 



