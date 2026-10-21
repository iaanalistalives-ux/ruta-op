# CLAUDE.md — Ruta de la OP (ruta-op)

Las reglas generales de trabajo están en el repo privado `lives-instrucciones` (CLAUDE.md). Este archivo solo describe esta herramienta.

## Qué hace
`index.html` es un **calendario de OPs** de solo lectura: junta lo **registrado** (real) y lo **programado** de todas las herramientas LIVES, por etapa: Pedido (OP creada), Corte, Costura, Acabados, Auditoría, Encajado, Despacho y Segundas (estas se registran por mes, sin día).
- Barra superior: búsqueda (OP, grupo, estilo o PO) con sugerencias desde 3 caracteres, cliente, Mes/Año, ‹ ›, Hoy y chips para prender o apagar etapas. El enlace se puede compartir (`#q=…&cliente=…&m=YYYY-MM`).
- Vista Mes: grilla lunes a domingo con las OP distintas por etapa (relleno = real, borde punteado = programado). Panel "Día" con los registros (hasta 500) y panel "Segundas del mes".
- Vista Año: 12 tarjetas con barras por etapa, comparadas contra el mes con más OP de esa etapa.
- **Ruta de una OP** (búsqueda de 4 a 6 dígitos): ficha (cliente, grupo, estilo, colores, PO, pedido, destino, tela) y una tarjeta por etapa con ✓ real, ◷ programado o – sin registro, con detalle propio (auditorías y rechazadas, prendas cortadas, último reporte de encajado, segundas por mes).
- Excel LIVES: resúmenes del período, por etapa, auditorías de Calidad Manufactura con % de rechazadas, la ruta completa de la OP buscada y detalle de eventos.

## Base de datos (Supabase lives-datos)
- Una sola puerta: `ruta_op(p_accion, p)` con las acciones `eventos` (por rango de fechas), `meses` (por año), `ruta` (una OP), `buscar` y `clientes`.
- Lee `ruta_op_ev` y `ruta_op_info`, y `cat_clientes` para el selector de cliente. Los eventos vienen de lo que registran las otras herramientas (auditorías de Calidad Manufactura, liquidación de corte, fotos de auditorías de taller, inspección de corte, encajado, segundas).
- No usa Storage. No guarda nada.

## Quién la usa
Según las entradas por el portal de los últimos 30 días al 21/10/2026: 1 persona (Datos e IA).

## Quién puede ver
Solo lectura; no tiene permisos propios.

## Pendientes vistos al escribir esto (21/10/2026)
- Código sin uso: `pintarKpis()` (los KPIs nunca se pintan) y el "pulso" del mes, desactivado con `if(false)`.
