# Checkpoint 2 — Modelo de datos y medidas DAX

**Autora:** Gina Rossi  
**Archivo de Power BI:** `Rossi_Gina_Checkpoint2.pbix`

## Objetivo

En esta preentrega continué el trabajo de limpieza y transformación del checkpoint anterior. Construí el modelo de relaciones, una tabla calendario y cinco medidas DAX para analizar las ventas y compararlas con el año anterior.

## Modelo de datos

`Fact_Ventas` es la tabla de hechos. Las cuatro relaciones están activas, tienen cardinalidad de uno a varios (1:*) y usan una sola dirección de filtro.

| Tabla del lado «1» | Tabla del lado «varios» |
| --- | --- |
| `Dim_Clientes[id_cliente]` | `Fact_Ventas[id_cliente]` |
| `Dim_Productos[id_producto]` | `Fact_Ventas[id_producto]` |
| `Dim_Categorias[id_categoria]` | `Dim_Productos[id_categoria]` |
| `Dim_Fechas[Date]` | `Fact_Ventas[fecha_venta]` |

Para relacionar productos con categorías, incorporé `id_categoria` a `Dim_Productos` mediante una combinación en Power Query entre `categoria` y `nombre_categoria`.

También creé `Dim_Fechas` con DAX, la marqué como tabla de fechas y agregué columnas de año, mes, trimestre y semana. Ordené `Mes Nombre` mediante `Mes Número` para mostrar los meses cronológicamente.

## Medidas DAX

Las cinco medidas están agrupadas en la tabla `_Medidas`:

| Medida | Descripción |
| --- | --- |
| `Total Ventas` | Suma el importe de las ventas. |
| `Ventas Online` | Calcula las ventas del canal Online mediante `CALCULATE`. |
| `Ventas YTD` | Acumula las ventas desde el inicio de cada año con `TOTALYTD`. |
| `Ventas LY` | Obtiene las ventas del mismo período del año anterior con `SAMEPERIODLASTYEAR`. |
| `% Crecimiento Anual` | Compara las ventas actuales con las del año anterior mediante `VAR` y `DIVIDE`. |

## Validación

Creé una página llamada **Validación** con una matriz que muestra los meses en las filas, los años en las columnas y las medidas `Total Ventas`, `Ventas YTD`, `Ventas LY` y `% Crecimiento Anual` en los valores.

Comprobé que:

- En enero de 2024, `Ventas YTD` y `Total Ventas` coinciden en **3.018,00**.
- `Ventas LY` de enero de 2024 es **2.967,50**, igual a `Total Ventas` de enero de 2023.
- El crecimiento de enero de 2024 frente a enero de 2023 es **1,70 %**.
- `Ventas LY` aparece en blanco durante 2023 porque no hay datos de 2022.
- El acumulado de 2024 llega a **18.814,00** en julio, el último mes con ventas de 2024 en el conjunto de datos.

La comparación anual de 2024 corresponde a los meses disponibles de ese año.
