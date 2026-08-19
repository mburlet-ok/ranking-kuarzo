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
- 2026-08-18 (7): **RCV corregido**: el usuario pasó la facturación total de Radio con Vos —
  May $173.129.278,78 · Jun $176.632.584,61 · Jul $170.584.051,34. Mar/Abr vuelven a la serie original
  ($84,0M / $160,0M). O sea que el total de la hoja RCV de la grilla ($12–22M/mes) es solo la parte que
  factura Kuarzo, NO la facturación de la radio: para este informe NO sirve. Segundos de May–Jul derivados
  del $/seg efectivo de Abril ($1.006).
- 2026-08-18 (8): **MITRE y LA 100 con dato real** pasado por el usuario: AM (Mitre) $6.300M y FM (La 100)
  $5.184M de **enero a junio** — el reparto entre ambas da 54,9% / 45,1%, que confirma el "55 y 45" que
  mencionó. Como el dato es un total de 6 meses y no un mes a mes, se cargó el **promedio mensual plano**:
  Mitre $1.050M/mes (188.544 seg a $5.569) y La 100 $864M/mes (146.242 seg a $5.908), Mar–Jun. Julio queda
  s/d (el dato llega hasta junio). Antes el informe las tenía en $1,2–1,6B/mes (monitor) y con La 100 arriba
  de Mitre; ahora Mitre queda primera, como corresponde al 55/45. Si aparece el desglose mes a mes, cambiar
  el plano por los valores reales.
- 2026-08-18 (9): **Rankings reordenados.** Antes las tablas iban fijas por Abril, así que con 5 meses
  cargados el orden no se correspondía con lo que se ve (ej. Canal 26 debajo de Cinecanal). Ahora
  `buildSection()` ordena por **promedio mensual** (no por total, porque las filas no tienen los mismos
  meses cargados: ordenar por total castigaba a Mitre/La 100, que no tienen Julio). Se agregó columna
  "Prom. mes" (promedio + subtítulo "N meses · total") y **todas las columnas son clickeables para
  reordenar** (`ordenar(cat,key)` + estado en `SORT`); las filas sin dato en la columna elegida van
  siempre al final. Se sacó la columna "Var. Mar→Abr" de la tabla (queda en los KPIs).
- 2026-08-19: **Radios May–Jul con segundos reales** de `radios a hoy.xlsx` (mismo formato "Parte Control"
  que el de canales; vehículos con prefijo AM-/FM-). Inversión = segundos reales × el $/seg de cada emisora.
  Cubre RADIO 10, RIVADAVIA, ASPEN, POP (FM-POP RADIO), VALE y BLUE. **No cubre MEGA ni ROCK AND POP**
  (siguen proyectados y en s/d en Julio) ni MITRE/LA 100 (van con el dato del usuario: $6.300M y $5.184M
  ene–jun). Con esto la solapa Radios queda 10 de 12 emisoras con dato real.
- 2026-08-19 (2): `radios a hoy.xlsx` se generó con **solo 6 vehículos en el filtro** (hoja "Resumen":
  AM-RIVADAVIA, FM-ASPEN, AM-RADIO 10, FM-POP RADIO, FM-VALE, FM-BLUE). **No hay forma de sacar los
  segundos reales de MITRE ni LA 100 de ese archivo**: hay que pedir el export de nuevo agregando
  "RA / AM-MITRE" y "RA / FM-LA 100" (y de paso MEGA y ROCK AND POP, que tampoco están).
  Mientras tanto, las cantidades **derivadas** (calculadas como plata ÷ $/seg o ÷ precio efectivo de Abril,
  no medidas por el monitor) se muestran con **≈** en cursiva: campo `est:[meses]` por fila. Hoy están
  marcadas: los 9 programas Kuarzo de TV (May–Jul), KZO y CANAL 13 en Canales, y MITRE, LA 100 y RCV en Radios.
- 2026-08-19 (3): sacada la solapa **Digital** completa (pestaña, contenedor, `buildDigital()` y su llamada
  en `showContent`). Eran datos sueltos de Febrero 2026 (share de sitios, anunciantes y media mix) que no
  seguían el formato mes a mes del resto del informe. Quedan cuatro solapas: TV Aire, Streaming, Canales y Radios.
- 2026-08-19 (4): la variación ahora es **último mes contra el anterior**, no contra Marzo. Por fila,
  `varTot()` toma los dos últimos meses **con dato de esa fila** (muestra "Jul/Jun", "Jun/May", etc.), así
  las que no tienen Julio comparan Jun contra May en vez de quedar sin dato. En los KPIs quedó una sola
  tarjeta "Var. <mes ant.> → <último>", calculada **solo sobre las filas que tienen los dos meses**
  (indica cuántas son) — si no, Julio parcial contra Junio completo mostraría una caída falsa.
- 2026-08-19 (5): agregado `vercel.json` con `Cache-Control: public, max-age=0, must-revalidate` para todo
  el sitio — sin eso Vercel/el navegador servían la versión vieja después de cada deploy y parecía que los
  cambios no se habían aplicado. Además el encabezado muestra "actualizado dd/mm hh:mm" tomado de
  `document.lastModified`, para poder confirmar de un vistazo si se está viendo la última versión.
- 2026-08-19 (6): alta de **CANAL 9** en Canales con $1.200M de facturación, cargado en **Julio** (mismo
  criterio que CANAL 13, que también es aire y no está en el parte de control). Queda sin `$/seg` ni
  segundos: falta que el usuario pase el valor por segundo para completarlos, igual que hizo con los
  $20.000 de Canal 13.
- 2026-08-19 (7): **LA NACION + recalculada a $6.000/seg** (antes $8.142) en los cinco meses, con los mismos
  segundos. Baja de $4,9B a $4,9B de total... (Mar $852,0M · Abr $878,2M · May $1.272,3M · Jun $997,4M ·
  Jul $856,2M) y cae del 4º al 6º puesto del ranking de Canales. Con esto queda en 3,4% de la tarifa de
  lista del monitor, dentro de la banda de TN/C5N/A24 (2,3–2,8%); antes estaba en 4,7%, que era el desvío
  que se había marcado.
- 2026-08-19 (8): auditadas TODAS nuestras filas contra las grillas: coinciden exacto con la suma por
  programa, salvo **CORTA POR LOZANO y CUESTION DE PESO en Marzo**, que seguían con el número del monitor
  ($471,1M y $159,7M) porque las hojas de programa de Marzo no los tienen. Corregidos con la **hoja FC de
  Marzo**: $377,0M y $149,2M. Ninguna fila nuestra (programas, KZO, Urbana, RCV) se calcula como
  segundos × valor promedio: la plata siempre sale de la grilla o del dato del usuario, y la cantidad se
  deriva de esa plata (por eso va con ≈).
- 2026-08-19 (9): **KZO 100% real** (plata de la hoja FC de cada mes: $46,1M · $45,8M · $59,4M · $58,2M · $72,1M): plata de la grilla y segundos MEDIDOS — Mar/Abr del monitor
  original (70.000 y 75.000) y May–Jul del parte de control de `canales a hoy.xlsx` (175.127 / 137.633 /
  84.638). El $/seg pasa a ser el efectivo real de cada mes ($658, $587, $341, $421, $825) en vez del
  $627 fijo. Se le sacó el marcador `est`.
- 2026-08-19 (10): KZO pasó de la suma de la hoja KZO TANDA a los **INGRESOS de la hoja FC** de cada mes
  (diferencias chicas salvo Julio: $69,8M → $72,1M). Ojo: FC y las hojas de programa siguen sin coincidir
  en GH, POLEMICA y BIENVENIDOS (la línea de FC es "segs + tanda") — esos tres siguen con la suma de la
  grilla por programa; falta que el usuario defina cuál manda.
- 2026-08-19 (11): **TODOS nuestros programas pasan a la hoja FC** (INGRESOS del mes, decisión del usuario),
  dejando de usar la suma de las hojas de programa. Los que cambian: GRAN HERMANO (Mar $1.244,7→$1.265,6M,
  Abr $1.168,6→$1.214,0M, Jul $1.007,8→$1.016,8M), ES MI SUEÑO, TODO COCINADO, POLEMICA (Abr $40,8→$50,8M)
  y sobre todo **BIENVENIDOS A GANAR**, que en FC es "segs + tanda" y sube de ~$60M a ~$120M por mes.
  A LA BARBARROSA sale de la línea **GEORGINA** de la FC. Mapeo de fila→línea FC en el commit.
  Las cantidades estimadas se recalcularon con el nuevo precio efectivo de Abril.
- 2026-08-19 (12): nueva solapa **Información** (`buildInfo()`), pensada para ir acumulando los datos de
  contexto que pasa el usuario. Todo el contenido vive en la constante `INFO` (titulares, mercado, canales,
  radios, notas) — para agregar algo nuevo se toca solo ese objeto. Contiene: caída −10% nominal / −40% real,
  15 de 18 rubros peor que hace un año, situación de laboratorios / consumo masivo / bancos / pauta pública,
  presupuestos reforecasteados; tabla de canales facturación vs prometido (Canal 13 $3.500M vs $5.000M
  prometidos, TN $3.000M vs $4.500M, América $1.500M tanda y $2.300M con PNTs, Canal 9 $1.200M y $2.000M,
  Magazine $50M); Mitre/La 100 ene–jun con el reparto 55/45; y la nota de Telefe con los paquetes del Mundial
  hasta septiembre. El banner de proyección se oculta en esta solapa.
