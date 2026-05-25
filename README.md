# 📊 CDO Analytics — Expreso Brasilia

Tablero ejecutivo de seguimiento operativo · Central de Operaciones

🔗 **Ver en vivo:** `https://tu-usuario.github.io/tu-repo/`

---

## Archivos del repositorio

| Archivo | Descripción |
|---------|-------------|
| `index.html` | Dashboard completo (HTML + CSS + JS inline) |
| `datos.csv` | **Datos principales** — métricas por operador |
| `audios.csv` | **Datos de audios** — envíos 2025–2026 |
| `sw.js` | Service Worker (PWA / offline) |
| `manifest.json` | Manifiesto de la app |

---

## Módulos del tablero

| Módulo | Descripción |
|--------|-------------|
| 🏠 Resumen General | KPIs globales, tendencia multimétrica, heatmap |
| 📞 Llamadas | Análisis completo de la métrica de llamadas |
| ✉️ Correos | Análisis completo de la métrica de correos |
| 🔔 Alertas | Análisis completo de la métrica de alertas |
| 🔄 Trasbordos | KPI nuevo — volumen y ranking por operador |
| 🔊 Audios | Envíos masivos y dirigidos, estándares, operadores |
| 👥 Operadores | Scorecard general, radar multiindicador |

---

## Actualizar datos

### `datos.csv` — métricas principales

Columnas requeridas (exactas, con tilde):
```
ID,OPERADOR,LLAMADAS,CORREOS,ALERTAS,AUDIOS,TRANSBORDOS,MES,MES Num,AÑO,PLATAFORMA
```

**Reglas:**
- `MES` en mayúsculas: `ENERO`, `FEBRERO`, … `DICIEMBRE`
- `MES Num`: número del mes (1–12)
- `PLATAFORMA`: `MICHELIN` o `WIZENZ`
- Valores numéricos con punto decimal: `1.25`
- Campos vacíos: dejar en blanco (no poner 0 si no hay dato)

### `audios.csv` — envíos de audios

Columnas requeridas:
```
OPERADOR,ESTANDAR,TIPO,MES,AÑO
```

- `TIPO`: `MASIVO` o `DIRIGIDO`
- `OPERADOR`: nombre en formato `Nombre Apellido`

---

## Cómo convertir el Excel a CSV

Desde Python (script reutilizable):

```python
import pandas as pd

# datos.csv
df = pd.read_excel('DATOS_BI_CENTRAL_COMPLETO.xlsx', sheet_name='RESUMEN')
out = df[['ID','OPERADOR','LLAMADAS','CORREOS','ALERTAS','AUDIOS','TRANSBORDOS','MES','MES Num','AÑO','PLATAFORMA']]
out.to_csv('datos.csv', index=False, float_format='%.3f', na_rep='')

# audios.csv
df2 = pd.read_excel('ENVIO_DE_AUDIOS_2025-2026.xlsx', sheet_name='ENVIOS 2025-2026')
df2[['Creador','ESTANDAR','TIPO DE ENVIO','Mes','Año']].rename(
    columns={'Creador':'OPERADOR','TIPO DE ENVIO':'TIPO','Mes':'MES','Año':'AÑO'}
).to_csv('audios.csv', index=False, na_rep='')

print('Listo.')
```

---

## Despliegue en GitHub Pages

1. Ir a **Settings → Pages**
2. Source: `Deploy from a branch`
3. Branch: `main` / `(root)`
4. Guardar → en ~2 min el tablero estará activo

---

## Paleta de colores

| Elemento | Color |
|----------|-------|
| Llamadas | `#1B56D4` Azul corporativo |
| Correos | `#0B7F59` Verde |
| Alertas | `#B45309` Ámbar |
| Trasbordos | `#6B3FC8` Púrpura |
| Audios | `#0E7490` Teal |
| Sidebar | `#0A1628` Azul marino |
