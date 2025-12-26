# Diccionario de Datos - Hoja General
## Dashboard Creadores de Prosperidad

---

## 📊 RESUMEN DE LA HOJA

| Atributo | Valor |
|----------|-------|
| **ID** | `general` |
| **Título** | Vista General |
| **Icono** | `fa-chart-line` |
| **Función de renderizado** | `renderGeneralSheet()` |

---

## 🔗 FUENTE DE DATOS

| Atributo | Valor |
|----------|-------|
| **Origen** | Google Sheets (CSV público) |
| **URL** | `https://docs.google.com/spreadsheets/d/e/2PACX-1vQWN6hZhglRb3xq_EtW5WkutefYhmJ6b8jb1hNyV1L4q5p2iuyYWUBSkSze1vXpVUQyoNkOk4S8MFi0/pub?gid=739894217&single=true&output=csv` |
| **Caché** | 5 minutos |
| **Parser** | PapaParse (con fallback manual) |

---

## 🎛️ FILTROS

### 1. Filtro de Fecha Inicio
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterDateFrom` |
| **Tipo** | `input[type="date"]` |
| **Valor por defecto** | Primer día del mes actual |
| **Columna filtrada** | `A.  FECHA R&P` |
| **Formato de columna** | `D/M/YYYY` (ej: `22/12/2025`) |

### 2. Filtro de Fecha Fin
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterDateTo` |
| **Tipo** | `input[type="date"]` |
| **Valor por defecto** | Fecha actual |
| **Columna filtrada** | `A. FECHA R&P` |
| **Formato de columna** | `M/D/YYYY` |

### 3. Accesos Rápidos de Fecha
| Botón | Rango de Fechas |
|-------|-----------------|
| Este Mes | 1° día del mes actual → Hoy |
| Mes Anterior | 1° día del mes anterior → Último día del mes anterior |
| Este Año | 1° de enero del año actual → Hoy |
| Todo | `1900-01-01` → `2099-12-31` |

### 4. Filtro de Programa
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterProgramInput` |
| **Tipo** | Searchable Select (dropdown con búsqueda) |
| **Columna filtrada** | `PROGRAMA` |
| **Comportamiento dinámico** | Se actualiza según filtros de Fecha y Año |
| **Valores disponibles** | Todos los programas únicos con ventas > 0 en el rango filtrado |

### 5. Filtro de Año Cierre
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterYear` |
| **Tipo** | `select` (dropdown) |
| **Columna filtrada** | `AÑO CIERRE DE VENTA` |
| **Valor por defecto** | "Todos" (vacío) |
| **Ordenamiento** | Descendente (más reciente primero) |

### 6. Exclusiones Globales
| Condición | Descripción |
|-----------|-------------|
| `ESTADO === 'Retirado'` | Excluye todos los registros de estudiantes retirados |

---

## 📈 KPIs (Indicadores Clave)

### Grid de KPIs
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `kpiGrid` |
| **Layout** | CSS Grid responsive (min 250px por tarjeta) |
| **Cantidad de KPIs** | 6 |

---

### KPI 1: Ventas Totales
| Atributo | Valor |
|----------|-------|
| **Etiqueta** | "Ventas Totales" |
| **Columna fuente** | `TOTAL VENTA *EXP COP*` |
| **Tipo de dato** | Numérico (moneda COP) |
| **Cálculo** | `SUM` de todos los registros filtrados |
| **Formato display** | Compacto (K, M, B) |
| **Formato tooltip** | Valor completo formateado (ej: `$ 1,234,567`) |

**Fórmula de cálculo:**
```javascript
const ventas = filtered.reduce((s, r) => s + parseNumber(r['TOTAL VENTA *EXP COP*']), 0);
```

---

### KPI 2: Recaudado
| Atributo | Valor |
|----------|-------|
| **Etiqueta** | "Recaudado" |
| **Columna fuente** | `NETO EXPRESADO EN PESOS` |
| **Tipo de dato** | Numérico (moneda COP) |
| **Cálculo** | `SUM` de todos los registros filtrados |
| **Formato display** | Compacto (K, M, B) |
| **Formato tooltip** | Valor completo formateado |

**Fórmula de cálculo:**
```javascript
const recaudo = filtered.reduce((s, r) => s + parseNumber(r['NETO EXPRESADO EN PESOS']), 0);
```

---

### KPI 3: Cartera Pendiente
| Atributo | Valor |
|----------|-------|
| **Etiqueta** | "Cartera Pendiente" |
| **Columna fuente** | `*A* PENDIENTE RECAUDO EXPRESADO EN PESOS` |
| **Columna filtro adicional** | `ESTADO PAGOS` |
| **Tipo de dato** | Numérico (moneda COP) |
| **Cálculo** | `SUM` donde `ESTADO PAGOS === 'PENDIENTE'` |
| **Formato display** | Compacto (K, M, B) |
| **Formato tooltip** | Valor completo formateado |

**Fórmula de cálculo:**
```javascript
const cartera = filtered
    .filter(r => r['ESTADO PAGOS'] === 'PENDIENTE')
    .reduce((s, r) => s + parseNumber(r['*A* PENDIENTE RECAUDO EXPRESADO EN PESOS']), 0);
```

---

### KPI 4: Programas
| Atributo | Valor |
|----------|-------|
| **Etiqueta** | "Programas" |
| **Columna fuente** | `PROGRAMA` |
| **Tipo de dato** | Contador (entero) |
| **Cálculo** | `COUNT DISTINCT` de programas |
| **Formato display** | Número entero |

**Fórmula de cálculo:**
```javascript
const programas = new Set(filtered.map(r => r.PROGRAMA)).size;
```

---

### KPI 5: Estudiantes
| Atributo | Valor |
|----------|-------|
| **Etiqueta** | "Estudiantes" |
| **Columna fuente** | `ESTUDIANTE` |
| **Tipo de dato** | Contador (entero) |
| **Cálculo** | `COUNT DISTINCT` de estudiantes |
| **Formato display** | Número entero |

**Fórmula de cálculo:**
```javascript
const estudiantes = new Set(filtered.map(r => r.ESTUDIANTE)).size;
```

---

### KPI 6: Ticket Promedio
| Atributo | Valor |
|----------|-------|
| **Etiqueta** | "Ticket Promedio" |
| **Columnas fuente** | `TOTAL VENTA *EXP COP*`, `PROGRAMA` |
| **Tipo de dato** | Numérico (moneda COP) |
| **Cálculo** | Ventas Totales ÷ Cantidad de Programas |
| **Formato display** | Compacto (K, M, B) |
| **Formato tooltip** | Valor completo formateado |

**Fórmula de cálculo:**
```javascript
const ticket = programas > 0 ? ventas / programas : 0;
```

---

## 📊 GRÁFICOS

### Gráfico: Ventas por Programa
| Atributo | Valor |
|----------|-------|
| **ID Canvas** | `chartVentasProgramas` |
| **Tipo** | `bar` (barras verticales) |
| **Librería** | Chart.js 3.9.1 |
| **Altura** | 400px |

#### Datos del Gráfico
| Atributo | Valor |
|----------|-------|
| **Eje X (labels)** | Nombres de programas (Top 10 + "OTROS") |
| **Eje Y (data)** | Suma de ventas por programa |
| **Columna para labels** | `PROGRAMA` |
| **Columna para valores** | `TOTAL VENTA *EXP COP*` |

#### Lógica de Agrupación
| Paso | Descripción |
|------|-------------|
| 1 | Agrupar registros por `PROGRAMA` |
| 2 | Sumar `TOTAL VENTA *EXP COP*` por programa |
| 3 | Filtrar programas con ventas > 0 |
| 4 | Ordenar de mayor a menor |
| 5 | Tomar Top 10 |
| 6 | Agrupar resto en "OTROS" |

#### Colores
| Elemento | Color |
|----------|-------|
| Barras Top 10 | `#301063` (púrpura oscuro) |
| Barra "OTROS" | `#B5A0D3` (púrpura claro) |

#### Interactividad
| Acción | Comportamiento |
|--------|----------------|
| Click en "OTROS" | Expande para mostrar todos los programas |
| Click en "OTROS" (expandido) | Contrae de vuelta a Top 10 + OTROS |
| Click en otras barras | Sin acción |

**Fórmula de cálculo:**
```javascript
const byProgram = {};
filtered.forEach(r => {
    byProgram[r.PROGRAMA] = (byProgram[r.PROGRAMA] || 0) + parseNumber(r['TOTAL VENTA *EXP COP*']);
});
```

---

## 🔘 BOTONES DE ACCIÓN

### Botón Refrescar
| Atributo | Valor |
|----------|-------|
| **Icono** | `fa-sync` |
| **Texto** | "Refrescar" |
| **Función** | `refreshData()` |
| **Comportamiento** | Limpia caché y recarga datos desde Google Sheets |

### Botón Descargar
| Atributo | Valor |
|----------|-------|
| **Icono** | `fa-download` |
| **Texto** | "Descargar" |
| **Función** | `exportData('csv')` |
| **Formato de salida** | CSV |
| **Nombre archivo** | `dashboard-export.csv` |

#### Columnas Exportadas
| Columna CSV | Columna Origen |
|-------------|----------------|
| ESTUDIANTE | `ESTUDIANTE` |
| PROGRAMA | `PROGRAMA` |
| VENTAS COP | `TOTAL VENTA *EXP COP*` |
| RECAUDADO COP | `NETO EXPRESADO EN PESOS` |
| PENDIENTE COP | `PENDIENTE RECAUDO INICIAL EXPRESADO TODO EN PESOS` |

---

## 📋 RESUMEN DE COLUMNAS UTILIZADAS

| Columna en Datos | Tipo | Uso en Hoja General |
|------------------|------|---------------------|
| `ESTUDIANTE` | String | KPI Estudiantes, Ticket Promedio, Exportación |
| `PROGRAMA` | String | KPI Programas, Gráfico Ventas, Filtro, Exportación |
| `TOTAL VENTA *EXP COP*` | Numérico | KPI Ventas Totales, Ticket Promedio, Gráfico Ventas, Exportación |
| `NETO EXPRESADO EN PESOS` | Numérico | KPI Recaudado, Exportación |
| `*A* PENDIENTE RECAUDO EXPRESADO EN PESOS` | Numérico | KPI Cartera Pendiente |
| `ESTADO PAGOS` | String | Filtro para Cartera Pendiente (`'PENDIENTE'`) |
| `ESTADO` | String | Exclusión global (`'Retirado'`) |
| `A.  FECHA R&P` | Fecha (D/M/YYYY) | Filtros de fecha |
| `AÑO CIERRE DE VENTA` | String | Filtro de Año |
| `PENDIENTE RECAUDO INICIAL EXPRESADO TODO EN PESOS` | Numérico | Exportación |

---

## 🔄 FLUJO DE DATOS

```
┌─────────────────────┐
│   Google Sheets     │
│   (CSV público)     │
└──────────┬──────────┘
           │ fetch + PapaParse
           ▼
┌─────────────────────┐
│    allData[]        │
│  (datos crudos)     │
└──────────┬──────────┘
           │ Filtros aplicados
           ▼
┌─────────────────────────────────────────────────┐
│              filtered[]                          │
│  Condiciones:                                    │
│  • ESTADO !== 'Retirado'                        │
│  • A.  FECHA R&P entre fechas                   │
│  • PROGRAMA === programa seleccionado (si hay)  │
│  • AÑO CIERRE DE VENTA === año (si hay)         │
└──────────┬──────────┘
           │
     ┌─────┴─────┬─────────────┬────────────┐
     ▼           ▼             ▼            ▼
┌─────────┐ ┌─────────┐ ┌───────────┐ ┌──────────┐
│  KPIs   │ │ Gráfico │ │  Filtros  │ │  Export  │
│  (6)    │ │ Barras  │ │ Dinámicos │ │   CSV    │
└─────────┘ └─────────┘ └───────────┘ └──────────┘
```

---

## ⚠️ VALIDACIONES Y CONSIDERACIONES

### Parseo de Números
```javascript
const parseNumber = (val) => {
    if (!val || val === "'" || val === '""') return 0;
    const cleaned = val.toString().replace(/[^\d.-]/g, '');
    const num = parseFloat(cleaned);
    return isNaN(num) ? 0 : num;
};
```

### Parseo de Fechas
- Formato esperado: `M/D/YYYY` (ej: `12/22/2025`)
- El mes es 1-indexed en los datos pero 0-indexed en JavaScript
- Se usa regex para extraer componentes: `/^(\d+)\/(\d+)\/(\d{4})$/`

### Formato de Moneda
- Locale: `es-CO`
- Currency: `COP`
- Sin decimales: `maximumFractionDigits: 0`

### Formato Compacto
| Rango | Sufijo | Ejemplo |
|-------|--------|---------|
| ≥ 1,000,000,000 | B | 1.2B |
| ≥ 1,000,000 | M | 1.2M |
| ≥ 1,000 | K | 1.2K |
| < 1,000 | (ninguno) | $ 999 |

---

## 📍 UBICACIÓN EN EL CÓDIGO

| Elemento | Línea Aproximada |
|----------|------------------|
| HTML de la hoja | 128-169 |
| Función `renderGeneralSheet()` | 741-891 |
| Función `setDateRange()` | 466-487 |
| Función `updateDynamicFilters('general')` | 634-676 |
| Función `populateFilterOptions()` | 415-464 |

---

*Documento generado: 2025-12-22*
*Dashboard: Creadores de Prosperidad v1.0*
