# Día 2/13 — Cap. 2: Promedio vs `p99` (*Tail Latency* y *Tail Latency Amplification*)

> **Referencia:** *Designing Data-Intensive Applications* (Martin Kleppmann y Chris Riccomini) · **Serie `@tlacuachedev`**
> **Versión web interactiva:** [Abrir HTML Interactivo](https://juliowhile.github.io/tlacuachedev-ddia/cap02-promedio-vs-p99.html) · **PDF (2 págs):** [Descargar PDF](./cap02-promedio-vs-p99.pdf)

---

## La idea central en 10 segundos

Un promedio de **20 ms** en tu dashboard no te dice cuántos usuarios sufren esperas de **4 segundos**. En producción, ese **1% más lento (`p99`)** suele ser tu **cliente VIP** (el que tiene más pedidos y más datos que consultar).

**Regla práctica del Cap. 2:** define tus SLAs y alertas sobre **`p95` y `p99`**, nunca sobre la media aritmética.

---

## Glosario rápido (8 términos clave)

- **Latencia:** tiempo total que tarda una petición desde que el cliente la envía hasta que recibe respuesta.
- **Percentil:** valor bajo el cual cae cierto porcentaje de peticiones ordenadas de la más rápida a la más lenta.
- **`p50` / Mediana:** punto medio real — la mitad de tus usuarios tardan menos que `p50` y la otra mitad más.
- **`p95` / `p99`:** umbral que cubre al 95% o 99% de las peticiones; `p99` expone el dolor del 1% más lento.
- **Tail Latency:** los percentiles altos (`p95`, `p99`, `p99.9`) en la "cola larga" de la distribución de tiempos.
- **Tail Latency Amplification:** fenómeno donde una pantalla que hace varias llamadas paralelas multiplica la probabilidad de tocar el `p99`.
- **Fan-Out:** una sola petición del usuario que dispara múltiples llamadas simultáneas a distintos servicios backend.
- **SLA / SLO:** objetivo interno de rendimiento (SLO) o compromiso contractual externo (SLA), por ejemplo `p99 < 500 ms`.

---

## Promedio vs Percentiles en producción

| Métrica | Qué mide realmente | Qué oculta / riesgo | Cuándo usarla |
| :--- | :--- | :--- | :--- |
| **Promedio (AVG)** | Suma de tiempos dividida entre N peticiones | Esconde picos extremos: 99 rápidas + 1 de 4 s apenas mueven el promedio | Solo reportes de capacidad/costos, **nunca** para UX ni alertas |
| **`p50` (Mediana)** | Experiencia del usuario típico | No muestra qué tan severa es la cola larga del 1%–5% | Referencia base del rendimiento típico |
| **`p95` / `p99`** | Límite real del 5% y 1% más lento (clientes VIP) | Requiere histogramas (no se pueden promediar entre nodos) | **SLOs, SLAs y alertas reales** en producción |

---

## Los 2 golpes reales de Kleppmann

1. **Tus mejores clientes caen en el `p99`:** el usuario nuevo con 0 pedidos carga en `12 ms`; el cliente VIP con 420 pedidos dispara consultas más pesadas y tarda `4,000 ms`. Al que más paga es justo al que corres.
2. **Tail Latency Amplification (`Fan-Out`):** si una pantalla llama en paralelo a 5 servicios (`Auth`, `Cart`, `Recs`, `Promo`, `Inventory`) y cada uno tiene 1% de probabilidad de tocar su `p99`, la probabilidad de que la pantalla completa sea lenta sube a **`1 - 0.99^5 ≈ 4.9%`**.

---

## Regla de alerta en producción (Prometheus)

```yaml
alert: HighTailLatencyVIP
expr: histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket[5m])) by (le)) > 0.5
for: 3m
annotations:
  summary: "p99 arriba de 500ms (clientes VIP afectados aunque AVG siga en 20ms)"
```

---

## 3 preguntas reales de entrevista (System Design)

1. **¿Por qué no basta medir el tiempo promedio (AVG) de una API?**
   Porque la latencia tiene distribución de cola larga: un 1% de peticiones lentas de 4 segundos apenas mueve el promedio, pero afecta de forma desproporcionada a los usuarios con más datos e historial (clientes VIP).
2. **¿Qué es *Tail Latency Amplification* en microservicios?**
   Cuando una pantalla depende de N llamadas en paralelo (*fan-out*), el usuario siempre espera al servicio más lento. Aunque cada servicio individual sea 99% rápido, la probabilidad de que al menos uno sea lento se multiplica.
3. **¿Se pueden promediar los `p99` de varios servidores para obtener el `p99` global?**
   **No.** Los percentiles no son promediables. Hay que agregar **histogramas** (buckets de latencia o HDR Histograms) y calcular el `p99` sobre la distribución combinada.

---

*Siguiente capítulo: **Día 3/13 — Cap. 3: Modelos de Datos (SQL vs NoSQL)**.*
