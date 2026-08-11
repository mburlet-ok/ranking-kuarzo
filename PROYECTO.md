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
