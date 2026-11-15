# Proyecto Final: Pipeline ETL con Arquitectura Medallion

**Autor:** Diego Quispe Vega
**Curso:** Ingeniería de Datos con Databricks
**Fecha:** Noviembre 2026

## 📝 Descripción del Proyecto
Este proyecto implementa un pipeline ETL (Extract, Transform, Load) utilizando **PySpark** y la **Arquitectura Medallion** (Bronze, Silver, Gold) en Databricks. Se procesaron dos fuentes de datos (Ventas de Ecommerce y Pedidos) para generar tablas agregadas de negocio, las cuales fueron visualizadas en un Dashboard final.

## 🏗️ Arquitectura Medallion Implementada
1. **Capa Bronze (Raw):** Ingesta inicial de los archivos CSV (`Ecommerce_Sales_Prediction_Dataset.csv` y `orders.csv`) en tablas Delta, manteniendo los datos crudos.
2. **Capa Silver (Transform):** Limpieza de datos, conversión de tipos (usando `try_cast` para tolerar errores en los encabezados), estandarización de nombres de columnas y eliminación de filas corruptas.
3. **Capa Gold (Load):** Agregación de datos para análisis de negocio. Se crearon dos tablas: `ventas_por_categoria` y `pedidos_por_hora`.

## 💻 Tecnologías Utilizadas
* **Databricks (Free Edition):** Plataforma principal para el procesamiento y gobierno de datos.
* **PySpark:** Para las transformaciones distribuidas.
* **Delta Lake:** Formato de almacenamiento de las tablas (ACID).
* **Databricks Workflows:** Para la orquestación de las tareas del ETL.
* **GitHub Actions:** Implementación de CI/CD para el despliegue automático.

## 📂 Estructura del Repositorio
* `datasets/`: Archivos CSV originales.
* `proceso/`: Notebooks de PySpark (`01_extract_bronze`, `02_transform_silver`, `03_load_gold`, `04_grants`).
* `seguridad/`: Scripts SQL para permisos (GRANT).
* `reversion/`: Scripts SQL para eliminación de tablas (DROP).
* `evidencias/`: Capturas de pantalla del Dashboard y ejecuciones exitosas.
* `.github/workflows/`: Archivo YAML (`deploy.yml`) para la automatización.

## ⚙️ Automatización CI/CD (GitHub Actions)
El pipeline de GitHub Actions se encarga de:
1. Conectarse a Databricks usando secretos seguros (`DATABRICKS_HOST` y `DATABRICKS_TOKEN`).
2. Subir la carpeta `proceso` al Workspace de Databricks.
3. Ejecutar el Job `ETL_Ecommerce_Medallion` de forma automática al hacer un `push` a la rama `main`.

## 📊 Visualización (Dashboard)
Se construyó un Dashboard en Databricks con dos gráficos principales:
* **Ingreso Total por Categoría:** Gráfico de barras mostrando qué categorías (Electronics, Sports, etc.) generan más ingresos.
* **Pedidos por Hora del Día:** Gráfico de líneas mostrando los picos de demanda (alta actividad entre las 10 y 15 horas).

*(Ver carpeta `evidencias` para las capturas de pantalla)*.
