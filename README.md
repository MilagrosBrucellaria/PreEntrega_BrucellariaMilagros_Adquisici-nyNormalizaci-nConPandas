# Pre-Entrega 2 - Integración de Datos de Ventas
## Objetivo
El objetivo de este proyecto es simular un escenario real donde la información de ventas proviene de distintas áreas de una organización y se encuentra almacenada en formatos diferentes.
Para ello se trabaja con:
- Un archivo CSV que contiene las transacciones de venta.
- Un archivo Excel que contiene el catálogo maestro de productos.

Posteriormente se realiza la limpieza de datos, la integración de ambas fuentes mediante un merge utilizando la columna `id_producto`, la creación de una variable calculada llamada `total_venta` y la exportación del resultado a formato Parquet.

## Estructura del repositorio

PreEntrega2_DSII/
│
├── transacciones.csv
├── productos.xlsx
├── ventas_integradas.parquet
├── preentrega_2_ventas.ipynb
├── requirements.txt
└── README.md
## Fuentes de datosñ
### transacciones.csv

Contiene el registro de ventas realizadas.

Columnas principales:

- id_producto
- cantidad
- fecha

### productos.xlsx

Contiene el catálogo maestro de productos.

Columnas principales:

- id_producto
- nombre_producto
- precio_unitario

---

## Tecnologías utilizadas

- Python
- Pandas
- OpenPyXL
- PyArrow
- Google Colab

---

## Librerías necesarias

```bash
pip install pandas openpyxl pyarrow
```

---

## Proceso realizado

### 1. Adquisición de datos

Se cargan dos fuentes de información:

- Archivo CSV de transacciones.
- Archivo Excel de productos.

### 2. Transformación

Se realizan las siguientes tareas:

- Conversión de `fecha` a tipo datetime.
- Conversión de columnas numéricas mediante `pd.to_numeric()`.
- Tratamiento de valores nulos.
- Validación de tipos de datos.

### 3. Integración de datos

Se realiza un merge utilizando:

```python
id_producto
```

como clave de unión entre ambas fuentes.

### 4. Normalización

Se crea la variable:

```python
total_venta = cantidad * precio_unitario
```

Esta columna representa el importe total de cada transacción.

### 5. Exportación

El dataset final se exporta en formato:

```text
ventas_integradas.parquet
```
para optimizar almacenamiento y procesamiento.

## Ejecución en Google Colab

### Conectar Google Drive

```python
from google.colab import drive
drive.mount('/content/drive')
```

### Definir ruta de trabajo

```python
ruta = "/content/drive/MyDrive/PreEntrega2_DSII"
```

### Cargar archivos

```python
transacciones = pd.read_csv(
    f"{ruta}/transacciones.csv"
)

productos = pd.read_excel(
    f"{ruta}/productos.xlsx",
    engine="openpyxl"
)

### Exportar resultado

```python
ventas.to_parquet(
    f"{ruta}/ventas_integradas.parquet",
    index=False,
    engine="pyarrow")

## Resultados obtenidos

✅ Carga de un archivo CSV.

✅ Carga de un archivo Excel.

✅ Corrección de tipos de datos.

✅ Manejo de valores nulos.

✅ Integración de ambas fuentes mediante merge.

✅ Creación de la columna `total_venta`.

✅ Generación de archivo final en formato Parquet.

✅ Proceso reproducible mediante Google Colab.

---

## Conclusión

Se desarrolló un flujo ETL básico utilizando Python y Pandas. El proceso permitió integrar información proveniente de distintos formatos, limpiar los datos, generar nuevas variables de negocio y exportar el resultado en un formato optimizado para análisis posteriores.
