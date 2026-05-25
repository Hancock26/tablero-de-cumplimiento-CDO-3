# 📘 Instructivo Completo — CDO Analytics
## Expreso Brasilia · Central de Operaciones

---

## ¿Qué es CDO Analytics?

CDO Analytics es un tablero ejecutivo web que centraliza el seguimiento de **indicadores de calidad y productividad** de los operadores de la Central de Operaciones. Consolida datos de dos plataformas (MICHELIN y WIZENZ), 12 meses del año y hasta 15 operadores en una sola vista interactiva orientada a gerencia.

---

## 1. Cómo acceder

### Desde computador (escritorio o portátil)
Abre el enlace del tablero en cualquier navegador moderno (Chrome, Edge, Firefox). No requiere instalación.

### Desde teléfono celular
1. Abre el enlace en **Chrome para Android** o **Safari para iPhone**
2. El diseño se adapta automáticamente a pantalla pequeña
3. **Para instalarlo como app** (acceso directo en pantalla de inicio):
   - **Android (Chrome):** Toca los tres puntos (⋮) → "Añadir a pantalla de inicio"
   - **iPhone (Safari):** Toca el ícono de compartir (□↑) → "Agregar a pantalla de inicio"
4. Una vez instalado, abre igual que cualquier otra app, sin necesidad del navegador
5. En la parte inferior aparece una **barra de navegación rápida** entre módulos

> La versión móvil tiene el mismo contenido que la de escritorio. Los filtros y gráficos funcionan igual, adaptados al tamaño de pantalla.

---

## 2. Estructura del tablero — los 7 módulos

### 🏠 Resumen General
Vista panorámica de toda la operación. Muestra los KPIs globales de las 5 métricas, la tendencia mensual de todas las métricas en un solo gráfico, el comparativo entre plataformas y un heatmap general.

### 📞 Llamadas · ✉️ Correos · 🔔 Alertas
Módulos independientes para cada métrica cuantitativa. Cada uno tiene sus propios KPIs, tendencia, ranking, comparativo de plataformas y heatmap. La lógica es idéntica para los tres.

### 🔄 Trasbordos
Módulo exclusivo para el KPI de trasbordos, que es un conteo (número entero) en lugar de porcentaje. Tiene su propio ranking y comparativo mensual.

### 🔊 Audios
Módulo de envíos de audios. Analiza los registros del sistema de despacho: cuántos masivos vs dirigidos, por qué operador, por qué estándar y en qué mes.

### 👥 Operadores
Vista consolidada de todos los operadores con su scorecard completo: las 3 métricas principales, trasbordos, score final y estado semafórico.

---

## 3. Los filtros — cómo funcionan

Cada módulo tiene una barra de filtros en la parte superior. Los filtros son **acumulativos**: puedes combinarlos todos al mismo tiempo.

| Filtro | Aplica en | Cómo usarlo |
|--------|-----------|-------------|
| **Operador** | Todos excepto Resumen | Ctrl+clic (o tap) para seleccionar varios |
| **Plataforma** | Llamadas, Correos, Alertas, Trasbordos | MICHELIN y/o WIZENZ |
| **Mes** | Todos | Selecciona uno o varios meses |
| **Año** | Todos | 2025 y/o 2026 |
| **Tipo de Audio** | Solo Audios | MASIVO y/o DIRIGIDO |

**Importante:** Para seleccionar varios valores en un filtro, mantén presionado **Ctrl** (Windows) o **Cmd** (Mac) mientras haces clic. En móvil, simplemente toca cada opción.

El botón **✕ Limpiar** elimina todos los filtros activos y vuelve a la vista completa.

---

## 4. Cómo se calculan los indicadores de porcentaje

Las métricas **Llamadas, Correos, Alertas y Audios** vienen del archivo `datos.csv` ya calculadas como porcentajes por operador y mes. El tablero no recalcula — **lee el valor directamente del CSV**.

### ¿Qué significa ese porcentaje?
Representa el **ratio de cumplimiento o actividad** del operador en esa métrica durante ese mes. Un valor de `1.25%` significa que ese operador registró un 1.25% en esa métrica en ese período.

### Promedio general (KPI principal de cada módulo)
```
Promedio general = Suma de todos los valores de la métrica ÷ Número de registros
```
Ejemplo: si hay 30 registros de Llamadas con valores entre 0.63% y 2.48%, el promedio es la suma de los 30 dividida entre 30.

### Variación vs mes anterior (flecha ▲▼)
```
Variación % = ((Promedio mes actual − Promedio mes anterior) ÷ Promedio mes anterior) × 100
```
- ▲ verde = el promedio subió respecto al mes anterior
- ▼ rojo = el promedio bajó

### Promedio por operador (en la tabla de detalle)
```
Promedio operador = Suma de sus valores en todos los meses seleccionados ÷ Número de meses
```
Cada fila de la tabla muestra este promedio y la barra de rendimiento relativo al operador con el valor más alto.

### Rendimiento relativo (barra en la tabla)
```
Rendimiento % = (Promedio del operador ÷ Valor máximo entre todos los operadores) × 100
```
El operador con el valor más alto siempre tiene barra al 100%. Los demás se escalan proporcionalmente. Sirve para comparar visualmente quién está más arriba o abajo dentro del grupo.

---

## 5. El Score Final (módulo Operadores)

El **Score** es un indicador compuesto que resume el desempeño general de cada operador en las 3 métricas cuantitativas principales.

### Fórmula
```
Score = Promedio de (Llamadas + Correos + Alertas) del operador
```
Solo se incluyen las métricas que tienen datos (si un operador no tiene Audios, no afecta su score).

### Ejemplo
| Operador | Llamadas | Correos | Alertas | Score |
|----------|----------|---------|---------|-------|
| Carlos Rosales | 1.37% | 0.56% | 2.50% | 1.47% |
| Edwin Giraldo | 0.63% | 0.72% | 0.26% | 0.54% |

El score de Carlos = (1.37 + 0.56 + 2.50) ÷ 3 = **1.47%**

---

## 6. El sistema de semáforos (estados)

Cada operador tiene un estado que resume su nivel de desempeño. Se calcula sobre el **promedio** o el **score** según el módulo.

| Estado | Color | Criterio (métricas %) | Criterio (Trasbordos) |
|--------|-------|----------------------|----------------------|
| **Bueno** | 🟢 Verde | ≥ 1.20% | ≥ 50 trasbordos |
| **Medio** | 🟡 Ámbar | Entre 0.60% y 1.19% | Entre 20 y 49 |
| **Bajo** | 🔴 Rojo | < 0.60% | < 20 trasbordos |

Estos umbrales están basados en los rangos observados en los datos históricos (mín 0.00%, máx 3.48%, promedio ~1.0%).

---

## 7. El Heatmap

El heatmap muestra una tabla de **operadores × meses** donde el color de cada celda indica el nivel del valor:

- **Color intenso** (azul oscuro, verde oscuro, etc.) = valor alto en esa celda
- **Color claro / blanco** = valor bajo
- **Celda gris "—"** = sin datos para ese operador en ese mes

La escala de color se ajusta dinámicamente al rango de los datos filtrados: la celda más alta siempre tiene el color más intenso, y la más baja el más claro.

---

## 8. Los gráficos — qué muestra cada uno

### Tendencia mensual (línea)
Muestra cómo evolucionó el **promedio del grupo** en cada mes. Útil para identificar si la operación va mejorando o empeorando en el tiempo.

### Ranking por operador (barras horizontales)
Ordena de mayor a menor el promedio de cada operador. El primero siempre tiene la barra más larga. Identifica rápidamente quién lidera y quién está rezagado.

### Comparativo plataformas × mes (barras agrupadas)
Compara MICHELIN vs WIZENZ mes a mes. Útil para ver si hay diferencias de desempeño entre las dos plataformas.

### Radar multiindicador (módulo Operadores)
Muestra los 6 mejores operadores en un gráfico de araña con los 3 ejes (Llamadas, Correos, Alertas). Un polígono más grande y equilibrado = mejor desempeño integral.

### Donut (módulo Audios)
Proporción visual entre audios Masivos y Dirigidos en la selección actual.

### Barras apiladas (módulo Audios)
Acumulado mensual de Masivos + Dirigidos. La altura total de cada barra = total de audios en ese mes.

---

## 9. Módulo Audios — explicación detallada

Los audios provienen del sistema de despacho y se clasifican en:

| Tipo | Descripción |
|------|-------------|
| **MASIVO** | Audio enviado a todos los conductores simultáneamente (recomendaciones generales, alertas de seguridad) |
| **DIRIGIDO** | Audio enviado a un conductor específico (fatiga detectada, celular, distracción) |

### Estándares de audio
Los estándares son las categorías temáticas de cada audio:
- **Recomendaciones generales** — mensajes de buenas prácticas
- **Use el cinturón de seguridad** — recordatorio de seguridad vial
- **Fatiga** — alerta por fatiga del conductor
- **No usar el celular** — alerta por uso del celular
- **Distancia de seguridad** — alerta por seguimiento cercano
- **Lente cubierto** — alerta por obstrucción de cámara

### Filtro de tipo de audio
En el módulo Audios puedes filtrar por **MASIVO**, **DIRIGIDO** o ambos. Al seleccionar solo uno, todos los gráficos, KPIs y rankings se recalculan mostrando únicamente ese tipo. Una barra de color en la parte superior confirma el filtro activo.

---

## 10. Trasbordos — qué es y cómo se mide

Los trasbordos son un **conteo de eventos** (número entero, no porcentaje). Representan la cantidad de trasbordos gestionados por cada operador en un período.

- **No todos los operadores tienen datos de trasbordos** — depende de si la plataforma registra este evento
- Los meses con datos son los que aparecen en el ranking; los demás no se muestran
- El semáforo de trasbordos usa umbrales distintos: ≥50 = Bueno, 20–49 = Medio, <20 = Bajo

---

## 11. Plataformas — MICHELIN vs WIZENZ

| Plataforma | Color | Característica |
|------------|-------|----------------|
| **MICHELIN** 🔵 | Azul | Registra Audios además de Llamadas, Correos y Alertas |
| **WIZENZ** 🟣 | Púrpura | Registra Trasbordos además de Llamadas, Correos y Alertas |

Algunos operadores están en ambas plataformas (aparecen con dos badges). En ese caso, sus datos de cada plataforma se muestran por separado en los filtros pero se consolidan en el promedio general.

---

## 12. Actualización de datos

Los datos se actualizan subiendo nuevos archivos CSV al repositorio de GitHub:

1. **`datos.csv`** — métricas de operadores (Llamadas, Correos, Alertas, Audios, Trasbordos)
2. **`audios.csv`** — registros de envíos de audios

Para convertir los Excel originales a CSV automáticamente, usa el script `convertir_datos.py`:
```bash
python convertir_datos.py
```
Esto genera los dos CSV listos para subir a GitHub. El tablero se actualiza en ~2 minutos.

---

## 13. Preguntas frecuentes

**¿Por qué algunos operadores no aparecen en Trasbordos?**
Porque no tienen registros de trasbordos en el período seleccionado. Los trasbordos solo aplican a ciertos operadores/plataformas.

**¿Por qué Audios solo aparece en algunos operadores?**
La columna AUDIOS en datos.csv solo tiene valores para operadores de MICHELIN. Los de WIZENZ no tienen esta métrica.

**¿Qué pasa si selecciono un mes donde un operador no tiene datos?**
El operador no aparece en la tabla de ese módulo/mes. Los filtros solo muestran registros que efectivamente existen en el CSV.

**¿El tablero funciona sin internet?**
Una vez cargado por primera vez, el Service Worker guarda los archivos en caché. Podrás ver los últimos datos aunque pierdas conexión, pero no se actualizará hasta reconectarte.

**¿Puedo ver el tablero en varios dispositivos?**
Sí. Es una página web, funciona en cualquier dispositivo con navegador. Los filtros no se sincronizan entre dispositivos — cada sesión es independiente.
