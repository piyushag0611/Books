# Chapter 1: Trade-offs in Data Systems Architecture

## Structure
Four core trade-offs:
- **OLTP vs OLAP** — operational (user-facing, point queries) vs analytical (aggregate, read-only copies)
- **Cloud vs Self-Hosting** — elasticity and outsourced ops vs control and compliance
- **Distributed vs Single-Node** — scale and fault tolerance vs simplicity and speed
- **Data Systems, Law & Society** — engineering decisions have legal and ethical consequences

## Key Takeaways
- "It depends" is the honest answer — the book deliberately avoids prescriptive rules
- Single-node is underrated; DuckDB/SQLite handle serious workloads (pushback against default distributed thinking)
- Ethics is in Chapter 1 on purpose — GDPR vs append-only logs is a real engineering constraint, not just legal paperwork

## Surprising
- Sustainability as a legitimate architectural reason to distribute: scheduling workloads when renewable energy is available

## Points of Confusion
- HTAP positioning is blurry — fraud detection is listed as an HTAP use case but sounds like what operational systems already do; the OLTP/HTAP/OLAP boundary isn't clean here

## Single-Node in the Wild
Real examples of single-node holding up in large setups:
- **SQLite** — per-user databases at WhatsApp scale; inside every mobile app
- **DuckDB** — Motherduck's core engine; replaces Spark for many analytical teams on one beefy machine
- **Redis (single instance)** — session storage and rate limiting at many companies; simplicity wins over HA
- **Postgres** — 37signals (Basecamp/Hey) moved off the cloud to bare-metal single-node Postgres: faster and cheaper
- **ClickHouse single-node** — handles billions of rows for mid-size analytics without a cluster

Common thread: if data fits on one machine and load is predictable, single-node wins on latency, cost, and ops simplicity.

## Terminology to Remember
- **System of record** — canonical/authoritative source of truth
- **Derived data system** — caches, indexes, ML models; reconstructable from source
- **ETL / ELT** — Extract-Transform-Load (or Load-then-Transform) pipeline from OLTP → warehouse
- **Data lake** — raw files, schema-on-read, flexible (Avro, Parquet), often on object storage
- **HTAP** — Hybrid Transactional/Analytical Processing; doesn't replace warehouses
- **Cloud native** — separates storage (S3) from compute; multitenant by design
- **Data minimization** — collect only what you need; counter to "big data" hoarding philosophy
