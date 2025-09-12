* [[Obiettivi di ETL]]
* [[GERARCHIE]]
* 

OLTP: on line transactional processing- sistema sorgente organizzati per velocizzare e otimizzare transazioni - [[INSERT INTO]] [[UPDATE]]  [[DELETE]]  

OLAP: on line analytical  processing - sistema analitico ottimizzato per velocizzare e semplificare interrogazioni  - [[SELECT]] [[JOIN]] [[WHERE]] [[GROUP BY 1]]

All'interno di una dataweb house le tabelle servono a otimizzare / aggregare le misure, filtare i dati [[WHERE]] [[HAVING]] e poi raggruppare dati [[GROUP BY 1]]

per questo motivo si dividono in fatti (le misure) e dimensioni  (anagrafiche)

il [[MODELLO DIMENSIONALE]] e' visto come ipercubo - con 4 dimensioni

1. I [[FATTI]] - eventi, cose successe (nel tempo) generalmente misurabili anche se non sempre - chiamate fact table
2. [[DIMENSIONI]] - sono gli assi di analisi che descrivono il contesto dei fatti

Elementi principali:
[[GERARCHIE]] : organizzazione in gerarchie che descrivono il percorso di aggregazione e servono per navigare nei dati

[[SCHEMATA]]: Star scheme vs Snowflake scheme che sono normalizzate o denormalizzate a seconda [[Normalizzazione Vs Denormalizzazione]]

[[NAMING CONVENTIONS]]: usare nomi comprensibili in modo che tutti possano comprendere immediatamente il ruolo degli oggetti che vedo 