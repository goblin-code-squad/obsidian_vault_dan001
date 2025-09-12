
# [[Normalizzazione]] vs [[Denormalizzazione]]


quando ampliamo stiamo normalizzando mettendo in piu' tabelle
quando denormalizzaimo invece concentriamo

il modello normalizzato ha meno join ma occupa piu' spazio
piu' vado lontanto dal fatto piu' il dato e' aggregato








---

### Query denormalizzata
```sql
-- 1 tabella piatta
SELECT cliente_nome, prodotto_nome, quantita
FROM report_vendite;
```

> 💡 **Tips per Obsidian**:
> - Attiva il plugin **Mermaid** (già incluso di default)
> - Clicca su "Preview" per vedere i diagrammi
> - Modifica facilmente le relazioni aggiungendo nuove entità

## ESEMPI PRATICI

### Query normalizzata (3 tabelle)
```sql
SELECT c.nome, p.nome, op.quantita
FROM clienti c
JOIN ordini o ON c.cliente_id = o.cliente_id
JOIN ordini_prodotti op ON o.ordine_id = op.ordine_id
JOIN prodotti p ON op.prodotto_id = p.prodotto_id;


## **Normalizzazione**
## (Ottimizzazione per integrità)

Processo di organizzazione dei dati per **ridurre ridondanze** e dipendenze.

### Livelli principali:
1. **1NF** (Forma Normale 1):  
   - Elimina gruppi ripetuti  
   - Tutti gli attributi atomici  

   
   | ordine_id | prodotto1 | prodotto2 | → | ordine_id | prodotto |
   |-----------|-----------|-----------|   |-----------|----------|
   | 1001         | Laptop     | Mouse       |   | 1001         | Laptop   |
   |                  |           |           |   | 1001      | Mouse    |



2. **2NF** (Forma Normale 2):  
   - Elimina dipendenze parziali (tutti gli attributi dipendono dalla PK completa)  

3. **3NF** (Forma Normale 3):  
   - Elimina dipendenze transitive (nessun attributo non-PK dipende da altri non-PK)  

### Esempio normalizzato (3NF):
```
┌───────────┐       ┌───────────────┐       ┌──────────────┐
│ Clienti   │       │ Ordini       │       │ Prodotti    │
├───────────┤       ├───────────────┤       ├──────────────┤
│ cliente_id│──────▶│ ordine_id    │──────▶│ prodotto_id │
│ nome      │       │ cliente_id   │       │ nome        │
│ email     │       │ data         │       │ prezzo      │
└───────────┘       └───────────────┘       └──────────────┘
                        ┌─────────────────────┘
                        ▼
                 ┌──────────────┐
                 │ Ordini_Prod  │
                 ├──────────────┤
                 │ ordine_id    │
                 │ prodotto_id  │
                 │ quantita     │
                 └──────────────┘
```

## 🚀 **Denormalizzazione** (Ottimizzazione per performance)
Introduzione **controllata** di ridondanze per migliorare velocità di lettura.

### Quando usarla:
- Reportistica frequente  
- Query complesse con molti JOIN  
- Dati storici immutabili  

### Esempio denormalizzato:
```
┌───────────────────────────────────────┐
│ Report_Vendite (vista materializzata) │
├───────────────────────────────────────┤
│ cliente_nome      │ prodotto_nome     │
│ cliente_email     │ prodotto_prezzo   │
│ ordine_data       │ quantita          │
│ totale_ordine     │ sconto_applicato  │
└───────────────────────────────────────┘
```

## 🔄 **Tradeoff**
| Caratteristica      | Normalizzato          | Denormalizzato       |
|---------------------|-----------------------|----------------------|
| **Integrità**       | ✅ Alta               | ❌ Rischio errori    |
| **Performance**     | ❌ Lento (molti JOIN) | ✅ Letture veloci    |
| **Spazio**          | ✅ Ottimizzato        | ❌ Occupa più spazio |
| **Manutenzione**    | ✅ Facile             | ❌ Complessa         |

## 💡 **Best Practice in Obsidian**
1. Per database concettuali:  
   ```markdown
   ## Modello Normalizzato
   ```sql
   CREATE TABLE clienti (
     cliente_id INT PRIMARY KEY,
     nome TEXT NOT NULL
   );
   ```

2. Per logiche di business:  
   ```markdown
   ## Vista Denormalizzata
   ```sql
   CREATE MATERIALIZED VIEW report_clienti AS
   SELECT c.nome, COUNT(o.ordine_id) as ordini_totali...
   ```

3. Usa diagrammi con Mermaid:  
   ```mermaid
   erDiagram
     CLIENTI ||--o{ ORDINI : "1:N"
     ORDINI }o--|| PRODOTTI : "M:N"
   ```

[[Normalizzazione]]
[[Denormalizzazione]]



