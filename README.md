# 🚀 Pipeline Completo del Laboratorio

## 1️⃣ Crear conexión HTTP en Microsoft Fabric
*Esta conexión permite que el pipeline acceda a los archivos CSV alojados en el repositorio público de GitHub del Ministerio de Ciencia de Chile.*

### 📍 Pasos para crear la conexión
1. Entra a Data Factory dentro de Microsoft Fabric.
2. Ve a la sección Administrar conexiones (Manage connections).
3. Haz clic en Nueva conexión (New connection).
4. Selecciona el tipo de conexión HTTP.

5. Configura los siguientes parámetros:  
    
      **Direccion url:** https://raw.githubusercontent.com/MinCiencia/Datos-CambioClimatico  
      **Nombre de la conexion:** http_conexion_github  
      **Tipo de autenticación:** Anónima.  
      **Nivel de privacidad:** Público  


  ![Conexión HTPP](images/conexion_htpp.png)

## 2️⃣ Notebook: nb_create_table_anios

Este notebook consulta la API REST de GitHub para listar dinámicamente los años disponibles (carpetas) y actualizar la tabla Delta tabla_anios con los nuevos años detectados, evitando duplicados.

📌 ¿Qué hace?

1. Llama a la API pública de GitHub:

https://api.github.com/repos/MinCiencia/Datos-CambioClimatico/contents/output/temperatura_dmc

2. Filtra carpetas que tengan un nombre numérico de 4 dígitos (e.g., 2020, 2021).

3. Verifica si la tabla tabla_anios ya existe:

4. Si existe, lee los años actuales. Si no existe, la crea vacía con la estructura correcta.

5. Detecta los años nuevos comparando contra lo ya almacenado.

6. Si encuentra nuevos, los agrega por append como Delta Table; si no, deja todo igual.

📓 [Ver notebook nb_create_table_annios.ipynb](nb_create_table_anios.ipynb)
