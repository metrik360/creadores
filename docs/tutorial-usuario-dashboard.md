# Tutorial del Dashboard - Creadores de Prosperidad

## Guía para Usuario Final

---

## 1. Introducción

### ¿Qué es este Dashboard?

El Dashboard Operacional de Creadores de Prosperidad es una herramienta web que te permite visualizar y analizar información de ventas, estudiantes, pagos y campañas de marketing en tiempo real.

### ¿Para qué sirve?

- Ver el estado general de ventas y recaudos
- Consultar información detallada de cada estudiante
- Analizar el rendimiento de las campañas de marketing
- Exportar datos para análisis adicionales

---

## 2. Cómo Acceder al Dashboard

1. Abre tu navegador web (Chrome, Firefox, Edge, Safari)
2. Ingresa la dirección URL proporcionada por tu equipo
3. Espera a que carguen los datos (verás los números aparecer en pantalla)

> **Nota:** Los datos se actualizan automáticamente desde una hoja de cálculo de Google cada vez que accedes.

---

## 3. Conociendo la Interfaz

### 3.1 Encabezado

En la parte superior encontrarás:

- El logo de **Creadores de Prosperidad**
- El título "Dashboard Operacional"

### 3.2 Pestañas de Navegación

Debajo del encabezado hay **3 pestañas** principales:

| Pestaña | Ícono | ¿Para qué sirve? |
|---------|-------|------------------|
| **General** | Gráfico de líneas | Vista panorámica de todas las ventas y estudiantes |
| **Estudiante** | Persona | Información detallada de un estudiante específico |
| **Marketing** | Megáfono | Análisis de campañas de marketing |

**Cómo cambiar de pestaña:** Simplemente haz clic sobre el nombre de la pestaña que deseas ver.

### 3.3 Pie de Página

Al final de la pantalla verás:

- La fecha y hora de la última actualización de datos
- El logo de MÉTRIK (desarrollador del dashboard)

---

## 4. Vista General - Análisis Global

### 4.1 Filtros Disponibles

#### Filtro de Fechas

Permite ver datos de un período específico:

- **Fecha Inicio:** Selecciona desde cuándo quieres ver datos
- **Fecha Fin:** Selecciona hasta cuándo quieres ver datos

**Botones de acceso rápido:**

| Botón | ¿Qué hace? |
|-------|------------|
| **Este Mes** | Muestra datos del mes actual |
| **Mes Anterior** | Muestra datos del mes pasado |
| **Este Año** | Muestra datos de todo el año en curso |
| **Todo** | Muestra todos los datos sin límite de fecha |

#### Filtro de Programa

1. Haz clic en el campo "Buscar programa..."
2. Escribe el nombre del programa que buscas
3. Selecciona el programa de la lista desplegable
4. Para quitar el filtro, haz clic en la "X" del campo

#### Filtro de Año de Cierre

1. Despliega la lista haciendo clic en "Todos los años"
2. Selecciona el año específico que deseas analizar

### 4.2 Tarjetas de Indicadores (KPIs)

Verás **6 tarjetas de colores** con información resumida:

| Tarjeta | Color | ¿Qué muestra? |
|---------|-------|---------------|
| **Ventas Totales** | Púrpura | Suma total de todas las ventas en pesos colombianos |
| **Recaudado** | Verde | Dinero que ya se ha cobrado efectivamente |
| **Cartera Pendiente** | Rojo | Dinero que falta por cobrar |
| **Programas** | Azul | Cantidad de programas diferentes vendidos |
| **Estudiantes** | Naranja | Cantidad de estudiantes únicos |
| **Ticket Promedio** | Celeste | Valor promedio por venta de programa |

> **Tip:** Si los números aparecen abreviados (ej: "150M"), pasa el cursor sobre la tarjeta para ver el valor completo (ej: "$150,000,000").

### 4.3 Gráfico de Ventas por Programa

Debajo de las tarjetas verás un **gráfico de barras** que muestra:

- Los 10 programas con más ventas
- Una barra llamada "OTROS" que agrupa los demás programas

**Funcionalidad especial:** Si haces clic en la barra "OTROS", el gráfico se expandirá mostrando TODOS los programas.

### 4.4 Tabla de Auditoría

Al final de la vista encontrarás una tabla detallada con:

| Columna | Descripción |
|---------|-------------|
| Estudiante | Nombre del estudiante |
| Programa | Nombre del programa adquirido |
| Fecha R&P | Fecha de registro y pago |
| Año Cierre | Año en que se cerró la venta |
| Venta Total | Valor total de la venta |
| Recaudado | Monto ya pagado |
| Pendiente | Monto que falta por pagar |
| Estado Pagos | PAGADO o PENDIENTE |
| Estado | Activo/Inactivo del estudiante |

---

## 5. Vista Estudiante - Detalle Individual

### 5.1 Cómo Buscar un Estudiante

1. Haz clic en el campo "Buscar estudiante..."
2. Escribe el nombre del estudiante (mínimo 2-3 letras)
3. La lista se filtrará automáticamente
4. Selecciona el estudiante de la lista

### 5.2 Indicadores del Estudiante

Verás **3 tarjetas** con la información del estudiante seleccionado:

| Tarjeta | ¿Qué muestra? |
|---------|---------------|
| **Total Vendido** | Suma de todas las ventas de ese estudiante |
| **Recaudado** | Cuánto ha pagado el estudiante |
| **Pendiente** | Cuánto debe todavía |

### 5.3 Gráfico de Desglose por Programa

Un **gráfico circular (dona)** que muestra la distribución de pagos entre los diferentes programas del estudiante.

### 5.4 Historial de Pagos

Tabla con todas las transacciones del estudiante:

- Programa
- Venta total
- Recaudado
- Pendiente
- Estado del pago

### 5.5 Validación de Consistencia

Esta sección especial **detecta posibles inconsistencias** en los datos de ventas:

| Indicador | Color | Significado |
|-----------|-------|-------------|
| **Válido** | Verde | Los datos coinciden perfectamente |
| **Margen ±5%** | Amarillo | Hay una diferencia menor al 5% (aceptable) |
| **Inconsistencia** | Rojo | Hay una diferencia mayor al 5% (revisar) |

---

## 6. Vista Marketing - Análisis de Campañas

### 6.1 Filtros Específicos de Marketing

Además de los filtros de fecha, programa y año, esta vista incluye:

**Filtro de Campaña:**

- Busca y selecciona una campaña específica
- Útil para analizar el rendimiento de cada campaña

### 6.2 Indicadores de Marketing

| Tarjeta | ¿Qué muestra? |
|---------|---------------|
| **Ventas Campaña** | Total vendido a través de campañas |
| **Recaudo** | Dinero cobrado de ventas por campaña |
| **Efectividad %** | Porcentaje de efectividad de las campañas |
| **Campañas** | Número de campañas activas |
| **Estudiantes** | Estudiantes captados por campaña |

### 6.3 Gráficos de Marketing

**Gráfico 1 - Ventas por Campaña:** Barras horizontales mostrando las campañas con más ventas.

**Gráfico 2 - Efectividad de Campañas:** Gráfico circular mostrando la distribución de efectividad.

### 6.4 Tabla de Detalle de Campañas

Información detallada de cada campaña:

- Nombre de la campaña
- Cantidad de estudiantes
- Ventas totales
- Monto recaudado
- Porcentaje de efectividad

---

## 7. Funciones Adicionales

### 7.1 Botón Refrescar

- **Ubicación:** Junto a los filtros
- **Función:** Actualiza los datos desde la fuente original
- **Cuándo usarlo:** Si crees que hay datos nuevos o si la información parece desactualizada

### 7.2 Botón Descargar

- **Ubicación:** Junto al botón Refrescar
- **Función:** Descarga los datos filtrados en formato CSV
- **El archivo incluye:** Estudiante, Programa, Ventas, Recaudado y Pendiente
- **Nombre del archivo:** `dashboard-export.csv`

> **Nota:** El archivo CSV se puede abrir con Excel, Google Sheets u otras hojas de cálculo.

---

## 8. Consejos y Mejores Prácticas

### Recomendaciones

1. **Usa los accesos rápidos de fecha** para análisis rápidos
2. **Pasa el cursor sobre las tarjetas** para ver valores exactos
3. **Haz clic en "OTROS"** en los gráficos para ver datos completos
4. **Exporta los datos** cuando necesites hacer análisis adicionales

### Consideraciones

1. Los datos se almacenan en caché por 5 minutos para mayor velocidad
2. Si los datos no parecen actualizados, usa el botón **Refrescar**
3. Los estudiantes con estado "Retirado" no aparecen en los análisis
4. Las campañas marcadas como "No Disponible" o "n/a" se excluyen automáticamente

---

## 9. Solución de Problemas Comunes

| Problema | Solución |
|----------|----------|
| No cargan los datos | Verifica tu conexión a internet y recarga la página |
| Los números parecen viejos | Haz clic en el botón Refrescar |
| No encuentro un estudiante | Asegúrate de escribir el nombre exactamente como está registrado |
| El gráfico está vacío | Verifica que los filtros aplicados tengan datos disponibles |
| La descarga no funciona | Intenta con otro navegador (Chrome recomendado) |

---

## 10. Glosario de Términos

| Término | Definición |
|---------|------------|
| **Ventas Totales** | Suma del valor de todos los programas vendidos |
| **Recaudado** | Dinero efectivamente cobrado |
| **Cartera Pendiente** | Dinero vendido pero aún no cobrado |
| **Ticket Promedio** | Valor promedio de cada venta (Ventas ÷ Programas) |
| **Efectividad** | Qué tan bien convierte una campaña (ventas logradas vs esfuerzo) |
| **R&P** | Registro y Pago - Fecha en que se formalizó la venta |
| **CSV** | Formato de archivo de datos separados por comas |

---

**¿Tienes dudas adicionales?** Contacta al equipo de soporte de MÉTRIK.
