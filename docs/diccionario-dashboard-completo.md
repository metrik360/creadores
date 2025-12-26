# Diccionario de Datos Completo
## Dashboard Creadores de Prosperidad

---

## 📋 INFORMACIÓN GENERAL

| Atributo | Valor |
|----------|-------|
| **Nombre** | MÉTRIK Dashboard - Creadores de Prosperidad |
| **Archivo** | `creadores/index.html` |
| **Hojas** | General, Estudiante, Marketing |

---

## 🔗 FUENTE DE DATOS

| Atributo | Valor |
|----------|-------|
| **Origen** | Google Sheets (CSV público) |
| **URL** | `https://docs.google.com/spreadsheets/d/e/2PACX-1vQWN6hZhglRb3xq_EtW5WkutefYhmJ6b8jb1hNyV1L4q5p2iuyYWUBSkSze1vXpVUQyoNkOk4S8MFi0/pub?gid=739894217&single=true&output=csv` |
| **Caché** | 5 minutos |
| **Parser** | PapaParse (con fallback manual) |

---

## 📊 COLUMNAS DE DATOS UTILIZADAS

| Columna | Tipo | Hojas que la usan |
|---------|------|-------------------|
| `ESTUDIANTE` | String | General, Estudiante, Marketing |
| `PROGRAMA` | String | General, Estudiante, Marketing |
| `TOTAL VENTA *EXP COP*` | Numérico | General, Estudiante, Marketing |
| `NETO EXPRESADO EN PESOS` | Numérico | General, Estudiante, Marketing |
| `*A* PENDIENTE RECAUDO EXPRESADO EN PESOS` | Numérico | General, Estudiante |
| `ESTADO PAGOS` | String | General, Estudiante |
| `ESTADO` | String | General, Estudiante, Marketing |
| `A.  FECHA R&P` | Fecha (D/M/YYYY) | General, Marketing |
| `AÑO CIERRE DE VENTA` | String | General, Estudiante, Marketing |
| `CAMPAÑA( Juli)` | String | Marketing |
| `$R & PROY exp pesos` | Numérico | Estudiante (Validación) |
| `PENDIENTE RECAUDO INICIAL EXPRESADO TODO EN PESOS` | Numérico | General (Exportación) |

---

# 📄 HOJA 1: GENERAL

## Descripción
Vista general del dashboard con KPIs principales, gráfico de ventas por programa y tabla de auditoría.

| Atributo | Valor |
|----------|-------|
| **ID** | `general` |
| **Icono** | `fa-chart-line` |
| **Función** | `renderGeneralSheet()` |

---

## Filtros

### Filtro de Fecha Inicio
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterDateFrom` |
| **Tipo** | `input[type="date"]` |
| **Columna filtrada** | `A.  FECHA R&P` |
| **Formato** | `D/M/YYYY` |

### Filtro de Fecha Fin
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterDateTo` |
| **Tipo** | `input[type="date"]` |
| **Columna filtrada** | `A.  FECHA R&P` |
| **Formato** | `D/M/YYYY` |

### Accesos Rápidos
| Botón | Rango |
|-------|-------|
| Este Mes | 1° día del mes actual → Hoy |
| Mes Anterior | 1° día del mes anterior → Último día |
| Este Año | 1° de enero → Hoy |
| Todo | Sin filtro de fecha |

### Filtro de Programa
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterProgramInput` |
| **Tipo** | Searchable Select |
| **Columna filtrada** | `PROGRAMA` |

### Filtro de Año Cierre
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterYear` |
| **Tipo** | Select dropdown |
| **Columna filtrada** | `AÑO CIERRE DE VENTA` |

### Exclusiones Globales
- `ESTADO === 'Retirado'` → Excluido
- Registros sin fecha válida cuando hay filtro activo → Excluidos

---

## KPIs

| KPI | Columna(s) | Cálculo |
|-----|------------|---------|
| **Ventas Totales** | `TOTAL VENTA *EXP COP*` | SUM |
| **Recaudado** | `NETO EXPRESADO EN PESOS` | SUM |
| **Cartera Pendiente** | `*A* PENDIENTE RECAUDO EXPRESADO EN PESOS` | SUM donde `ESTADO PAGOS = 'PENDIENTE'` |
| **Programas** | `PROGRAMA` | COUNT DISTINCT |
| **Estudiantes** | `ESTUDIANTE` | COUNT DISTINCT |
| **Ticket Promedio** | `TOTAL VENTA *EXP COP*` ÷ Programas | Ventas / Programas |

---

## Gráfico: Ventas por Programa

| Atributo | Valor |
|----------|-------|
| **ID Canvas** | `chartVentasProgramas` |
| **Tipo** | Barras verticales |
| **Eje X** | `PROGRAMA` (Top 10 + "OTROS") |
| **Eje Y** | SUM(`TOTAL VENTA *EXP COP*`) |
| **Interactividad** | Click en "OTROS" expande/contrae |

---

## Tabla de Auditoría

| Columna | Fuente |
|---------|--------|
| # | Índice |
| Estudiante | `ESTUDIANTE` |
| Programa | `PROGRAMA` |
| Fecha R&P | `A.  FECHA R&P` |
| Año Cierre | `AÑO CIERRE DE VENTA` |
| Venta Total | `TOTAL VENTA *EXP COP*` |
| Recaudado | `NETO EXPRESADO EN PESOS` |
| Pendiente | `*A* PENDIENTE RECAUDO EXPRESADO EN PESOS` |
| Estado Pagos | `ESTADO PAGOS` |
| Estado | `ESTADO` |

**Resumen de Totales:**
- Ventas, Recaudado, Cartera, Programas, Estudiantes, Ticket

---

# 📄 HOJA 2: ESTUDIANTE

## Descripción
Detalle individual de estudiantes con historial de pagos y validación de consistencia de ventas.

| Atributo | Valor |
|----------|-------|
| **ID** | `estudiante` |
| **Icono** | `fa-user` |
| **Función** | `renderEstudianteSheet()` |

---

## Filtros

### Filtro de Estudiante
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterEstudianteInput` |
| **Tipo** | Searchable Select |
| **Columna filtrada** | `ESTUDIANTE` |

### Filtro de Año Cierre
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterYearEst` |
| **Tipo** | Select dropdown |
| **Columna filtrada** | `AÑO CIERRE DE VENTA` |

### Exclusiones
- `ESTADO === 'Retirado'` → Excluido

---

## Panel de Información del Estudiante

| Campo | Fuente |
|-------|--------|
| Estudiante | `ESTUDIANTE` (seleccionado) |
| Estado | `ESTADO` (ACTIVO si alguno es "Activo") |
| Programas | COUNT DISTINCT de `PROGRAMA` |

---

## KPIs

| KPI | Columna(s) | Cálculo |
|-----|------------|---------|
| **Total Vendido** | `TOTAL VENTA *EXP COP*` | SUM del estudiante |
| **Recaudado** | `NETO EXPRESADO EN PESOS` | SUM del estudiante |
| **Pendiente** | `*A* PENDIENTE RECAUDO EXPRESADO EN PESOS` | SUM del estudiante |

---

## Gráfico: Desglose por Programa

| Atributo | Valor |
|----------|-------|
| **ID Canvas** | `chartEstProgramas` |
| **Tipo** | Dona (doughnut) |
| **Datos** | SUM(`NETO EXPRESADO EN PESOS`) por `PROGRAMA` |

---

## Tabla: Historial de Pagos

| Columna | Fuente/Cálculo |
|---------|----------------|
| Programa | `PROGRAMA` |
| Venta Total | SUM(`TOTAL VENTA *EXP COP*`) por programa |
| Pagado | SUM(`NETO EXPRESADO EN PESOS`) por programa |
| Pendiente | SUM(`*A* PENDIENTE RECAUDO EXPRESADO EN PESOS`) por programa |
| % Pagado | (Pagado / Venta Total) × 100 |
| Estado | "Pagado" si Pendiente = 0, sino "Pendiente" |

---

## Tabla: Validación de Consistencia de Ventas

| Columna | Fuente/Cálculo |
|---------|----------------|
| Estudiante | `ESTUDIANTE` |
| Programa | `PROGRAMA` |
| TOTAL VENTA *EXP COP* | SUM del valor |
| $R & PROY exp pesos | SUM de `$R & PROY exp pesos` |
| Diferencia (%) | ((R&P - Venta) / Venta) × 100 |
| Estado | Válido (0%), Margen ±5% (±5%), Inconsistencia (>5%) |

**Estados de Validación:**
| Estado | Condición | Color |
|--------|-----------|-------|
| Válido | Diferencia = 0% | 🟢 Verde |
| Margen ±5% | -5% ≤ Diferencia ≤ 5% | 🟠 Naranja |
| Inconsistencia | Diferencia > 5% o < -5% | 🔴 Rojo |

---

# 📄 HOJA 3: MARKETING

## Descripción
Análisis de campañas de marketing con métricas de ventas y efectividad.

| Atributo | Valor |
|----------|-------|
| **ID** | `marketing` |
| **Icono** | `fa-bullhorn` |
| **Función** | `renderMarketingSheet()` |

---

## Filtros

### Filtro de Fecha Inicio
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterDateFromMkt` |
| **Tipo** | `input[type="date"]` |
| **Columna filtrada** | `A.  FECHA R&P` |
| **Formato** | `D/M/YYYY` |

### Filtro de Fecha Fin
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterDateToMkt` |
| **Tipo** | `input[type="date"]` |
| **Columna filtrada** | `A.  FECHA R&P` |
| **Formato** | `D/M/YYYY` |

### Accesos Rápidos
| Botón | Rango |
|-------|-------|
| Este Mes | 1° día del mes actual → Hoy |
| Mes Anterior | 1° día del mes anterior → Último día |
| Este Año | 1° de enero → Hoy |
| Todo | Sin filtro de fecha |

### Filtro de Programa
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterProgramMktInput` |
| **Tipo** | Searchable Select |
| **Columna filtrada** | `PROGRAMA` |

### Filtro de Año Cierre
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterYearMkt` |
| **Tipo** | Select dropdown |
| **Columna filtrada** | `AÑO CIERRE DE VENTA` |

### Filtro de Campaña
| Atributo | Valor |
|----------|-------|
| **ID HTML** | `filterCampaignInput` |
| **Tipo** | Searchable Select |
| **Columna filtrada** | `CAMPAÑA( Juli)` |

### Exclusiones
- `ESTADO === 'Retirado'` → Excluido
- `CAMPAÑA( Juli)` vacío, "No Disponible", o contiene "n/a" → Excluido
- Registros sin fecha válida cuando hay filtro activo → Excluidos

---

## KPIs

| KPI | Columna(s) | Cálculo |
|-----|------------|---------|
| **Ventas Campaña** | `TOTAL VENTA *EXP COP*` | SUM de registros con campaña válida |
| **Recaudo** | `NETO EXPRESADO EN PESOS` | SUM |
| **Efectividad** | Ventas Campaña ÷ Ventas Total Empresa | Porcentaje de impacto |
| **Campañas** | `CAMPAÑA( Juli)` | COUNT DISTINCT |
| **Estudiantes** | `ESTUDIANTE` | COUNT DISTINCT |

---

## Gráfico: Ventas por Campaña

| Atributo | Valor |
|----------|-------|
| **ID Canvas** | `chartVentasCampanas` |
| **Tipo** | Barras horizontales |
| **Eje Y** | `CAMPAÑA( Juli)` (Top 10 + "OTRAS") |
| **Eje X** | SUM(`TOTAL VENTA *EXP COP*`) |
| **Interactividad** | Click en "OTRAS" expande/contrae |

---

## Gráfico: Efectividad de Campañas

| Atributo | Valor |
|----------|-------|
| **ID Canvas** | `chartEfectividad` |
| **Tipo** | Pie (pastel) |
| **Datos** | SUM(`TOTAL VENTA *EXP COP*`) por campaña (Top 5 + "OTRAS") |
| **Interactividad** | Click en "OTRAS" expande/contrae |

---

## Tabla: Detalle de Campañas

| Columna | Fuente/Cálculo |
|---------|----------------|
| Campaña | `CAMPAÑA( Juli)` |
| Estudiantes | COUNT DISTINCT de `ESTUDIANTE` por campaña |
| Ventas Totales | SUM(`TOTAL VENTA *EXP COP*`) por campaña |
| Recaudado | SUM(`NETO EXPRESADO EN PESOS`) por campaña |
| % Efectividad | (Ventas Campaña / Ventas Total Filtrado) × 100 |

---

# 🔧 FUNCIONES GLOBALES

## Formato de Números
```javascript
function fmt(v) {
    return new Intl.NumberFormat('es-CO', {
        style: 'currency',
        currency: 'COP',
        maximumFractionDigits: 0
    }).format(parseFloat(v) || 0);
}
```

## Formato Compacto
| Rango | Sufijo | Ejemplo |
|-------|--------|---------|
| ≥ 1,000,000,000 | B | 1.2B |
| ≥ 1,000,000 | M | 1.2M |
| ≥ 1,000 | K | 1.2K |
| < 1,000 | (ninguno) | $ 999 |

## Parseo de Fechas
- **Columna:** `A.  FECHA R&P`
- **Formato:** `D/M/YYYY` (ej: `22/12/2025`)
- **Regex:** `/^(\d+)\/(\d+)\/(\d{4})$/`

## Parseo de Números
```javascript
function parseNumber(val) {
    if (!val || val === "'" || val === '""') return 0;
    const cleaned = val.toString().replace(/[^\d.-]/g, '');
    const num = parseFloat(cleaned);
    return isNaN(num) ? 0 : num;
}
```

---

# 📤 EXPORTACIÓN

## Función: exportData()
| Atributo | Valor |
|----------|-------|
| **Formato** | CSV |
| **Nombre archivo** | `dashboard-export.csv` |

### Columnas Exportadas
| Columna CSV | Columna Origen |
|-------------|----------------|
| ESTUDIANTE | `ESTUDIANTE` |
| PROGRAMA | `PROGRAMA` |
| VENTAS COP | `TOTAL VENTA *EXP COP*` |
| RECAUDADO COP | `NETO EXPRESADO EN PESOS` |
| PENDIENTE COP | `PENDIENTE RECAUDO INICIAL EXPRESADO TODO EN PESOS` |

---

*Documento generado: 2025-12-22*
*Dashboard: Creadores de Prosperidad v1.0*
