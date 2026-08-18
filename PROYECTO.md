# Ranking Medios 2026

## Sobre el proyecto
Dashboard HTML interactivo que muestra rankings de inversión publicitaria en programas de TV y medios argentinos. Los datos vienen de un Excel con info mes a mes (Enero, Febrero, Marzo) + Acumulado 2026.

## Archivos
- `index.html` — Dashboard principal
- `data.xlsx` — Excel fuente con los datos originales

## Datos que contiene
- **Ranking de anunciantes** (clientes) con inversión total
- **Ranking de vendedores**
- **Inversión por programa de TV**: A la Barbarrosa, Bienvenidos a Ganar, Corta por Lozano, Cuestión de Peso, Escuela de Cocina, KZO, La Cocina Rebelde, Medios, Polémica en el Bar, The Balls, Gran Hermano, Es mi Sueño, Todo Cocinado
- Febrero, Marzo y Acumulado tienen vista Con/Sin Gran Hermano

## Stack
- HTML/CSS/JS puro (single page)
- Chart.js para gráficos
- Diseño dark mode profesional

## Objetivo
- Se va a hostear online para compartir con el jefe via link
- Se va a ir agregando más información

## Notas
- (acá vamos anotando cambios y pendientes)
- 2026-08: Agregados MAY, JUN y JUL 2026 (ranking clientes/vendedores/programas + Con/Sin GH),
  reconstruidos desde las grillas de facturación (`COSTO MENSUAL` = cant × costo neto por cliente).
  Acumulado 2026 (Ene–Jul, $18.11B) y Evolución actualizados. Tanda de Gran Hermano sin vendedor → TELEFE (como Abril).
  Julio salió de `GRILLA JULIO 2026 30.xlsx` (el archivo completo con grillas); el primer archivo de Julio
  venía incompleto (solo hoja resumen).
- 2026-08-18: `facturacion.html` pasa de "Marzo vs Abril" a 4 meses (Marzo · Abril · Mayo · Junio 2026)
  en TV Aire, Streaming, Cable y Radios. **Mayo y Junio son proyección**, no datos reales:
  Mayo = Abril +10% y Junio = Mayo −25%, aplicado a inversión y cantidades (PNTs / segundos) de cada
  medio; los costos por salida/segundo quedan iguales a Abril. Las columnas de meses proyectados van
  marcadas ("proy.") + banner de aviso arriba. Tablas unificadas en `buildSection()`; se agregó columna
  "Var. Mar→Jun" y buscador por fila. Fix: en Cable el `$/Seg` mostraba "-" (usaba `p.valor`, que no
  existe en esas filas) — ahora usa `abr_costo`.
- 2026-08-18 (2): pestaña "TV Cable" renombrada a **"Canales"** (ahora mezcla cable y aire) y se sumó
  **Julio 2026 con datos reales**, por ahora solo dos canales: TN $3.000M (200.000 seg @ $15.000/seg) y
  CANAL 13 $3.500M (175.000 seg @ $20.000/seg) — segundos calculados como facturación ÷ costo por segundo.
  CANAL 13 es alta nueva en la tabla de Canales (no tiene Mar–Jun; el CANAL 13 de Streaming es otra fila).
  `buildSection()` ahora muestra la columna de un mes solo si algún medio tiene dato (`s/d` si falta) y
  marca el KPI como "(parcial x/y)" cuando el mes está incompleto. Para cargar el resto de Julio: agregar
  `jul_costo`/`jul_cant`/`jul_inv` a cada fila del `DATA`.
- 2026-08-18 (3): en `facturacion.html` **nuestros programas y medios pasan a facturación real de las
  grillas** (fuente: `DATA.<mes>.programs` de `ranking.html`, Mar–Jul 2026): GH, ES MI SUEÑO, CORTA POR
  LOZANO, LA COCINA REBELDE, A LA BARBARROSA, CUESTION DE PESO, TODO COCINADO, BIENVENIDOS A GANAR,
  POLEMICA EN EL BAR y KZO (en Canales) + altas MIX TV y ARRIBA AMERICA. Esas filas llevan badge KUARZO
  y NO usan la proyección +10%/−25%; el resto del mercado (monitor) sigue proyectado y se ve con fondo
  violeta. PNTs de May–Jul derivados del precio efectivo de Abril (grilla da plata, no PNTs); en Canales
  los segundos se recalculan como plata ÷ costo/seg. Última columna pasó a "Var. vs Marzo" (contra el
  último mes con dato de cada fila, con el mes indicado al lado). **Sin dato de grilla 2026:** RCV,
  URBANA PLAY y ESCUELA DE COCINA (siguen proyectados / en cero); el bucket MEDIOS de las grillas no
  tiene fila en este informe.
