# Telecom X — Análisis de Cancelación de Clientes (Churn) | Challenge

Este repositorio contiene un proyecto de **análisis de evasión/cancelación de clientes (Churn)** para **Telecom X**.
El objetivo es **cargar, limpiar y explorar** los datos de clientes para identificar patrones asociados a la cancelación y generar insights que ayuden a futuras **estrategias de retención** y, posteriormente, a la construcción de **modelos predictivos**.

---

## Objetivo del proyecto

* Cargar datos de clientes desde una fuente en formato **JSON** (API/URL).
* Aplicar pasos de **ETL** (Extracción → Transformación → Datos listos para análisis).
* Realizar **EDA** (Análisis Exploratorio) con estadísticas descriptivas y visualizaciones.
* Elaborar un **informe final** con hallazgos e ideas de mejora para reducir churn.

---

## Dataset

* Formato: **JSON**
* Contenido principal:

  * Perfil del cliente (género, senior citizen, partner, dependents, tenure)
  * Servicios (telefonía, internet y servicios adicionales)
  * Cuenta (tipo de contrato, facturación, método de pago)
  * Cargos (mensual y total)
  * Variable objetivo: **Churn** (si el cliente canceló o no)

---

## ¿Qué se hizo durante el proyecto?

### 1) Extracción

* Se cargaron los datos desde un JSON público (API/URL).

### 2) Transformación / Limpieza

* Se aplanó el JSON con `pandas.json_normalize()` para obtener un DataFrame “en forma de tabla”.
* Se realizaron revisiones de calidad:

  * tipos de datos (`info()`, `dtypes`)
  * nulos, duplicados y valores vacíos (strings en blanco)
  * inconsistencias en categorías
* Correcciones principales:

  * Conversión de `Charges.Total` a numérico (venía como texto y con algunos valores vacíos).
  * Eliminación de filas con `Churn` vacío y filas con `Charges.Total` nulo (después de convertirlo).
  * Estandarización de variables binarias:

    * Conversión de **Yes/No** a **1/0**
    * Manejo de categorías como `"No internet service"` para evitar NaN al mapear
* Opcional:

  * Creación de `Cuentas_Diarias` como estimación de cobro diario (`Charges.Monthly / 30`)

### 3) EDA (Análisis Exploratorio)

* Estadísticas descriptivas (media, mediana, desviación estándar, min/max).
* Distribución de cancelación (conteo y porcentaje).
* Visualizaciones de cancelación por:

  * género
  * tipo de contrato
  * tipo de internet
  * método de pago
* Comparación de cancelación vs variables numéricas:

  * `tenure`
  * `Charges.Monthly`
  * `Charges.Total`

### 4) Informe final

* Dentro del notebook se incluye un reporte con:

  * Introducción
  * Limpieza y tratamiento
  * EDA + gráficos
  * Conclusiones e insights
  * Recomendaciones

---

## Contenido del repositorio

```text

TelecomX_LATAM.ipynb
raw
README.md
```

> Nota: Este proyecto fue desarrollado en **Google Colab**, por lo que puedes ejecutarlo sin instalar nada localmente.

---

## Cómo ejecutar (Google Colab)

1. Abre el notebook
2. Ejecuta las celdas de arriba hacia abajo.
3. El notebook realizará:

   * carga de datos
   * limpieza/transformación
   * gráficas de EDA
   * reporte final

---


## Posibles problemas comunes

* **NaN después de convertir Yes/No**:
  Algunas columnas incluyen valores como `"No internet service"` (no es exactamente `"No"`).
  Se reemplaza ese texto antes de convertir a 0/1.

* **Charges.Total como texto**:
  Puede venir como `object` y con valores vacíos; se convierte a numérico y se limpian nulos.

---

## Autor

Sergio Tadeo Carrillo Montoya (Data Science / ONE G9)

---

