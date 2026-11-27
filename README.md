<p align="center">
  <img src="./assets/logo_tlacuachedev.png" alt="Logo oficial @tlacuachedev" width="112" />
</p>

# tlacuachedev-ddia

Apuntes técnicos, cheatsheets interactivos (HTML) y PDFs descargables para la serie **13 días resumiendo *Designing Data-Intensive Applications*** (Martin Kleppmann y Chris Riccomini) de **`@tlacuachedev`**.

Cada capítulo está pensado para repasar en menos de 3 minutos antes de una entrevista de **System Design** o una discusión de arquitectura en producción.

## Mapa de la Temporada 1 (13 capítulos)

| Día | Parte | Capítulo | Tema principal | HTML Interactivo | Markdown | PDF | Estado |
| :---: | :---: | :--- | :--- | :---: | :---: | :---: | :---: |
| **01** | I | Cap. 1: Trade-offs de arquitectura | Monolito vs microservicios, fallos parciales y criterios para distribuir | [Abrir Web Interactiva](https://juliowhile.github.io/tlacuachedev-ddia/cap01-monolito-vs-microservicios.html) | [Ver MD](./cap01-monolito-vs-microservicios.md) | [Descargar PDF](./cap01-monolito-vs-microservicios.pdf) | Disponible |
| **02** | I | Cap. 2: Requisitos no funcionales | Promedio vs p99 (tail latency), VIPs y Tail Latency Amplification | [Abrir Web Interactiva](https://juliowhile.github.io/tlacuachedev-ddia/cap02-promedio-vs-p99.html) | [Ver MD](./cap02-promedio-vs-p99.md) | [Descargar PDF](./cap02-promedio-vs-p99.pdf) | Disponible |
| **03** | I | Cap. 3: Modelos de datos y consultas | SQL vs NoSQL (documentos y grafos), cuándo elegir cada uno | Próximamente | Próximamente | Próximamente | En cola |
| **04** | I | Cap. 4: Almacenamiento y recuperación | Índices, B-Trees vs LSM-Trees y almacenamiento columnar | Próximamente | Próximamente | Próximamente | En cola |
| **05** | I | Cap. 5: Codificación y evolución | JSON vs Protobuf/Avro y compatibilidad en despliegues | Próximamente | Próximamente | Próximamente | En cola |
| **06** | II | Cap. 6: Replicación | Líder-seguidor, multi-líder, lag de replicación y lecturas | Próximamente | Próximamente | Próximamente | En cola |
| **07** | II | Cap. 7: Sharding / Particionamiento | Key-range vs hash, hot spots y rebalanceo | Próximamente | Próximamente | Próximamente | En cola |
| **08** | II | Cap. 8: Transacciones | ACID real, Read Committed vs Serializable y doble cobro | Próximamente | Próximamente | Próximamente | En cola |
| **09** | II | Cap. 9: Problemas de sistemas distribuidos | Redes poco confiables, relojes y pausas de GC | Próximamente | Próximamente | Próximamente | En cola |
| **10** | II | Cap. 10: Consistencia y consenso | Linearizability, 2PC, Raft y Paxos | Próximamente | Próximamente | Próximamente | En cola |
| **11** | III | Cap. 11: Procesamiento por lotes | Filosofía Unix, MapReduce y flujos batch | Próximamente | Próximamente | Próximamente | En cola |
| **12** | III | Cap. 12: Procesamiento de streams | Event logs (Kafka), CDC y Event Sourcing | Próximamente | Próximamente | Próximamente | En cola |
| **13** | III | Cap. 13: Filosofía de sistemas streaming | Unbundling databases, dataflow e integridad end-to-end | Próximamente | Próximamente | Próximamente | En cola |

## Versión web interactiva (GitHub Pages)

Puedes abrir los cheatsheets directamente en tu navegador (con diagramas interactivos, glosario y botón para imprimir PDF):
- **[Cap. 1 · Monolito vs Microservicios (Web Interactiva)](https://juliowhile.github.io/tlacuachedev-ddia/cap01-monolito-vs-microservicios.html)**
- **[Cap. 2 · Promedio vs p99 / Tail Latency (Web Interactiva)](https://juliowhile.github.io/tlacuachedev-ddia/cap02-promedio-vs-p99.html)**

## Cómo usar estos cheatsheets para entrevistas

1. **Mira el video corto** del día en `@tlacuachedev` para fijar el modelo mental y el caso de producción.
2. **Abre la versión HTML interactiva** (o el PDF / Markdown) para comparar el flujo de Checkout con y sin `Idempotency-Key`, repasar números de referencia (`~100 ns` en RAM vs `200+ ms` en red) y la regla de decisión.
3. **Practica en voz alta** las 3 preguntas de entrevista al final de cada archivo. En una entrevista de System Design, mencionar el trade-off exacto (y cuándo *no* usar cierta arquitectura) vale más que recitar herramientas de moda.

## Dónde ver la serie completa

- **Instagram:** [@tlacuachedev](https://instagram.com/tlacuachedev)
- **TikTok:** [@tlacuachedev](https://tiktok.com/@tlacuachedev)
- **YouTube Shorts:** [@tlacuachedev](https://youtube.com/@tlacuachedev)

Si te sirve para tu próxima entrevista, deja una estrella en el repo para enterarte cuando subamos el **Día 2 (Promedio vs p99)**.

---

*Nota: estos apuntes son resúmenes didácticos originales de estudio inspirados en los temas de Designing Data-Intensive Applications (O'Reilly). No reproducen texto ni figuras del libro.*
