
Analisi Requisti > la scrive il Business
Analisi Fattibilita' > It la scrive - Business appprova
CHECKPOINT <> nel workflow

Analisi Funzionale > scrive IT > approva Business

Analisi Tecnica > IT

Documento di Rilascio - Script di rilascio in altenativa
- Manuale utente
- Manuale di esercizio

	Documento di V.A.T.
checkpoint

rilascio in produzione (Deploy)

Descriptive Analytics

Predictive Analytics

Prescriptive Analytics


```mermaid
---
title: Workflow Progetto
---
flowchart TD
	A[Analisi Requisiti - IT produce, Business Approva] --> B[Analisi fattibilita - IT produce, Business Aprova] --> C{Primo Checkpoint di controllo}
C --> E[Analisi funzionale - IT scrive, Bus Approva]
	C --> |Problemi vari| D[Molti progetti muoiono qui]
	E --> F[Analisi Tecnica - IT esegue]
	F --> G[Documento di Rilascio o anche Script di rilascio]
	G --> H[Documento di V.A.T]
	H --> I{Secondo Checkpoint}
	I --> L(Rilascio in Produzione / Deploy)
```