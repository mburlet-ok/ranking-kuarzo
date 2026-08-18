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
- 2026-08-18 (4): URBANA PLAY pasa a facturación real de la **hoja FC** (columna INGRESOS) de
  `\\Volumes\comercial\Facturacion\2026\0X- Facturacion <Mes> 2026.xlsx` — la hoja FC es el resumen del mes
  por programa/medio y es la fuente original de los valores Mar/Abr que ya tenía el informe. Urbana:
  Mar $939,4M · Abr $684,5M · May $732,0M · Jun $1.068,3M. Segundos de May/Jun derivados del $/seg efectivo
  de Abril ($4.183). Ojo: **RCV no tiene línea en FC** (sí una hoja RCV propia, cuyo TOTAL da $12,6M/$12,9M/
  $19,3M/$21,7M para Mar–Jun, muy por debajo de los $84M/$160M que muestra el informe). El archivo
  `07- Facturacion Julio 2026.xlsx` de esa carpeta NO tiene hoja FC (solo `Hoja1` con el detalle), así que
  Julio de Urbana quedó sin dato.
- 2026-08-18 (5): **RCV no figura en la hoja FC de ningún mes** (verificado Ene a Jul 2026: la FC lista
  ES MI SUEÑO, LCR, TC, BAG, CORTA, CDP, GEORGINA, GH, PB, ARRIBA AMERICA, KZO, MIXTV, URBANA PLAY y
  SEG+MEDIOS; en la primera solapa "Facturacion" solo aparecen filas `RCV - TANDA` / `RCV - PNT`).
  RCV se toma entonces de su **hoja RCV** (total TANDA + PNT) y los segundos de la columna
  "Total Segundos": Mar $12,6M/20.282s · Abr $12,9M/16.134s · May $19,3M/27.308s · Jun $21,7M/26.072s ·
  Jul $16,3M/43.092s. Antes el informe mostraba $84M/$160M para Mar/Abr (venían del monitor, no de las
  grillas). URBANA PLAY: FC + segundos "Seg. c/ Cargo" de la hoja URBANA; Jul $997,5M.
  **Julio completo está en `/Users/maxiburlet/Desktop/varios/GRILLA JULIO PARA EL CIERRE.xlsx`** (el
  `07- Facturacion Julio 2026.xlsx` de la carpeta comercial solo tiene `Hoja1`, sin FC ni hojas de programa).
  PENDIENTE: la FC y las grillas por programa no coinciden en GH, POLEMICA y BIENVENIDOS (la FC de
  BIENVENIDOS es "segs + tanda"); definir con el usuario cuál manda para el informe.
- 2026-08-18 (6): **Canales May–Jul con segundos reales** de `/Volumes/comercial/canales a hoy.xlsx`
  (hoja "Parte Control": un spot por fila, 01/05 a 31/07/2026, todos "Corte Comercial"; agrupar por
  Vehículo + mes sumando `Dur.Av.`). Inversión = segundos reales × el $/seg promedio que ya tenía cada
  canal. Cubre TN, LN+, C5N, A24, Canal 26, Cinecanal, Discovery, AMC y Magazine. **No cubre** CRONICA ni
  CIMEMAX (no están en el export → siguen proyectados) ni CANAL 13 (es aire; queda con los $3.500M de Julio
  que pasó el usuario). **KZO queda con FC**, NO con el monitor: el parte de control le da 175.127 seg ×
  $627 = $109,8M en Mayo contra $59,4M reales de FC. Validación: TN Mayo = 201.364 seg × $15.000 = **$3,02B**,
  que es exactamente los "3 mil millones" que el usuario había pasado para TN (los había cargado en Julio;
  Julio real da $1,90B con 126.741 seg). La etiqueta "proy." del encabezado ahora sale sola solo si más de
  la mitad de las filas de ese mes siguen proyectadas.
