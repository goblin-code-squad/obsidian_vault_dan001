
---

## Database Associativi: Riassunto Breve

### Cos'è un Database Associativo?

Un Database Associativo è un modello di dati (spesso implementato tramite **tabelle di congiunzione/bridge tables**) utilizzato per risolvere le **relazioni Molti-a-Molti (M:N)** tra due o più entità.

In un contesto di Data Warehouse o Database Relazionale, non puoi connettere direttamente una tabella A con molte righe di una tabella B, e viceversa. Il database associativo funge da **intermediario**.

### Struttura e Componenti Chiave

| Componente                       | Ruolo nel Modello                                                                 | Esempio                                  |
| -------------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------- |
| **Tabella A**                    | Entità base. Ha una sua chiave primaria.                                          | `DIM_Prodotto` (Chiave: `ID_Prodotto`)   |
| **Tabella B**                    | Seconda entità base. Ha una sua chiave primaria.                                  | `DIM_Categoria` (Chiave: `ID_Categoria`) |
| **Tabella Associativa (Bridge)** | Tabella **Molti-a-Molti**. Contiene **solo** le chiavi primarie delle due entità. | `Ass_Prodotto_Categoria`                 |

### Funzionamento nel DW (Contesto Data Warehouse)

1. **Risoluzione del M:N:** La tabella associativa trasforma la relazione M:N in **due relazioni Uno-a-Molti (1:N)**.
    
    - `DIM_Prodotto` **→ 1:N →** `Ass_Prodotto_Categoria`
        
    - `DIM_Categoria` **→ 1:N →** `Ass_Prodotto_Categoria`
        
2. **Conteggio Corretto (Anti-Double Counting):** È la soluzione principale al problema del **double counting** quando si tratta di attributi a multi-valore.
    
    - Se un Prodotto appartiene a 3 Categorie, la Tabella Fatto (`FACT_Vendite`) si collega **solo** alla tabella `DIM_Prodotto`.
        
    - Per analizzare le Vendite per Categoria, la query deve passare attraverso la tabella associativa (`FACT_Vendite` → `DIM_Prodotto` → `Ass_Prodotto_Categoria` → `DIM_Categoria`).
        
    - Questo assicura che il conteggio delle metriche di Fatto non venga duplicato.
        

### 💡 Esempio Pratico

- **Scenario:** Un prodotto (`Prodotto X`) è venduto sia come "Scarpa da Corsa" che come "Articolo Sportivo".
    
- **Problema senza Bridge:** Se colleghi `FACT_Vendite` direttamente a entrambe le categorie, la vendita di `Prodotto X` verrebbe contata due volte se raggruppi per categoria.
    
- **Soluzione con Bridge:** La `Ass_Prodotto_Categoria` ha due righe per `Prodotto X`. La `FACT_Vendite` si collega una sola volta a `Prodotto X`. La query di aggregazione gestisce il conteggio attraverso la tabella associativa.