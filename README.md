# S25 - Evidencia de aprendizaje 3: Creación de un Data Warehouse

### Autores:
- **Jean Carlos Páez Ramírez**  
- **Hernán Darío Borja Quiroz**  

### Docente:
- **Aharon Alexander Aguas Navarro**  
Especialista en Inteligencia de Negocios y Business Intelligence  

### Curso:
- **Inteligencia de Negocios**

**Programa:** Ingeniería en Desarrollo de Software y Datos  
**Facultad:** Ingeniería y Ciencias Agropecuarias  
**Institución Universitaria Digital de Antioquia**  
**2024**

---

## Introducción
En un entorno empresarial donde los datos son esenciales para la toma de decisiones, contar con un Data Warehouse optimizado es crucial. Este proyecto desarrolla un proceso completo de **ETL (Extracción, Transformación y Carga)**, utilizando como caso de estudio los datos de Jardinería Flor del Campo S.A. Se ilustra cómo gestionar y analizar datos estratégicos, enfocándonos en la identificación de patrones clave, como productos más vendidos, mediante un modelo estrella.

---

## Objetivos del Proyecto
### Objetivo General:
Desarrollar un proceso ETL eficiente para un Data Warehouse, optimizando el análisis de datos para Jardinería Flor del Campo S.A.

### Objetivos Específicos:
1. Extraer datos de una base de datos operativa hacia una base de staging.  
2. Transformar los datos para garantizar calidad, consistencia y preparación para el análisis.  
3. Cargar los datos transformados en un Data Mart utilizando un modelo estrella.  

---

## Planteamiento del Problema
Jardinería Flor del Campo S.A. enfrenta retos significativos en la gestión de datos:  
- **Acceso ineficiente:** La estructura actual dificulta la extracción rápida de información.  
- **Falta de integración:** Datos dispersos y no normalizados limitan los análisis coherentes.  
- **Calidad inconsistente:** Datos duplicados o erróneos afectan la toma de decisiones.  

---

## Propuesta de Solución
### Proceso ETL:
1. **Preparación:**  
   - Diseñar y verificar el modelo estrella.  
   - Validar la estructura y consistencia de las bases de datos origen y staging.  

2. **Extracción:**  
   - Realizar consultas SQL para extraer datos relevantes desde la base de datos "Jardinería".  
   - Transferir datos al staging.  

3. **Transformación:**  
   - Limpiar y normalizar datos para eliminar inconsistencias.  
   - Generar tablas de dimensiones y hechos siguiendo el modelo estrella.  

4. **Carga:**  
   - Transferir los datos transformados al Data Mart final, garantizando integridad y eficiencia.  

---

## Diseño del Modelo Estrella
El modelo estrella incluye:  
- **Dimensiones:** Producto, Cliente, Tiempo.  
- **Tabla de hechos:** Fact_Venta.  

**Enlace al modelo estrella:**  
[Ver diagrama en draw.io](https://drive.google.com/file/d/1yGUeJBWj3AUnplmQdDGnT4Q9oh-fpl0f/view?usp=sharing)

---

## Lista de Dimensiones Propuestas

### 1. Dimensión Producto:
- ID_Producto (Clave primaria)  
- Nombre, Categoría, Precio, Descripción  
- CódigoProducto, Cantidad_en_stock  

### 2. Dimensión Cliente:
- ID_Cliente (Clave primaria)  
- Nombre, Apellido, Teléfono, Dirección  
- Ciudad, País, Código Postal  

### 3. Dimensión Tiempo:
- ID_Tiempo (Clave primaria)  
- Fecha, Año, Mes, Día, Día_semana, Trimestre  

### Tabla de Hechos - Fact_Venta:
- ID_Venta (Clave primaria)  
- Claves foráneas: ID_Producto, ID_Cliente, ID_Tiempo  
- Cantidad, Monto_Total  

---

## Desarrollo del Proceso ETL

### 1. Extracción de Datos
- **Herramienta:** Microsoft Integration Services (SSIS).  
- **Conexiones:** Bases de datos "Jardinería" (origen) y "StagingJardinería" (destino).  
- **Flujo:**  
  - Limpieza de tablas destino mediante consultas TRUNCATE.  
  - Extracción de datos mediante consultas SQL.  

#### Ejemplo de consulta:
```sql
SELECT ID_Producto, Nombre, Categoría, Precio
FROM Producto
ORDER BY ID_Producto;
```

### 2. Transformación de Datos
- **Transformaciones aplicadas:**  
  - Limpieza de duplicados.  
  - Enriquecimiento con datos calculados.  
  - Normalización de formatos.  
- **Ejemplo de transformación:**
```sql
SELECT 
    p.ID_Producto,
    p.Nombre AS NombreProducto,
    c.Categoría AS CategoríaProducto,
    ISNULL(p.Descripción, 'Sin descripción') AS DescripciónProducto
FROM Producto p
JOIN Categoría c ON p.ID_Categoría = c.ID_Categoría;
```

### 3. Carga de Datos
- **Carga final:**  
  - Las tablas de dimensiones y la tabla de hechos se almacenan en el Data Mart para consultas analíticas avanzadas.  

---

## Resultados
- **Base de datos StagingJardinería:** Captura exitosa de datos clave desde la base operativa.  
- **Modelo estrella:** Dimensiones y tabla de hechos diseñadas para facilitar análisis eficientes.  
- **Transformaciones:** Datos limpios, normalizados y enriquecidos listos para análisis.  

### Captura del proceso:
![Flujo de datos sin errores](https://ibb.co/MNdrbKK)

---

## Conclusión
Este proyecto demuestra la importancia de un proceso ETL estructurado en la creación de un Data Warehouse. A través de un modelo estrella optimizado, Jardinería Flor del Campo S.A. ahora cuenta con herramientas analíticas para tomar decisiones estratégicas basadas en datos.  