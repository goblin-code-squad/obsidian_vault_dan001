Certamente! Ecco il testo sistemato con una formattazione ottimizzata per Obsidian, organizzato in sezioni logiche con markdown e elementi di collegamento tipici dell'app.

---

# Caricamento Dati: Modalità Full Refresh vs Incremental (Delta)

##  Definizione delle Modalità

### 🔄 Full Refresh
- **Operazione**: `DROP` della tabella di landing + copia integrale dalla sorgente
- **Utilizzo ideale**: 
	- Moli di dati sorgenti molto basse
	- Database di piccole dimensioni
- **Vantaggi**: Semplicità implementativa
- **Svantaggi**: Computazionalmente costoso per database grandi

###  Modalità Incremental/Delta
- **Scopo**: Inserimento solo dei dati nuovi/aggiornati dalla sorgente al database di landing (`nome_database_landing`)
- **Operazioni**:
	- Caricare solo le righe nuove
	- Aggiornare le righe esistenti
- **Strumento principale**: `MERGE` (anziché `DROP`)

##  Tecnica MERGE

### Cos'è la MERGE
Operazione che combina `UPDATE` e `INSERT` in un unico comando:
- **Aggiorna** le righe esistenti
- **Inserisce** le righe nuove

![[Pasted image 20251113154429.png]]

### Sintassi MERGE
```sql
MERGE INTO schema.tabella_landing AS target
USING tabella_sorgente AS source
ON target.chiave_id = source.chiave_id
```

###  Clausole Operative

#### WHEN MATCHED THEN
```sql
UPDATE SET
    campo1 = source.campo1,
    campo2 = source.campo2,
    ...
```

#### WHEN NOT MATCHED THEN
```sql
INSERT (colonna1, colonna2, ...)
VALUES (source.valore1, source.valore2, ...)
```

##  Considerazioni Critiche

### Attenzione ai Campi
- **Sequenza colonne**: Deve corrispondere tra sorgente e destinazione
- **Mappatura**: Corrispondenza precisa nei comandi `UPDATE SET`

### Gestione Dati Sorgente
**Problema**: Se USING carica l'intera tabella sorgente, si eseguono operazioni su tutti i record.

**Soluzioni**:
1. **Sorgente preparata**: La sorgente fornisce solo righe nuove/aggiornate
2. **Filtro temporale**: Utilizzo di timestamp (`last_date_modified`)

![[Pasted image 20251113165852.png]]

##  Implementazione Pratica

###  Filtro per Data
```sql
-- Filtrare la tabella sorgente sugli ultimi X giorni
WHERE data_modifica >= DATEADD(day, -7, GETDATE())
```

![[Pasted image 20251113171054.png]]

###  Esempio UPDATE
![[Pasted image 20251113171321.png]]

## Casi d'Uso Avanzati

###  Streaming Analytics
- **Scenario**: Caricamento continuo (ogni secondo)
- **Necessità**: Modalità delta obbligatoria
- **Motivazione**: Evitare perdite di performance con flussi dati intensivi

## Conclusioni
- **Preservazione storico**: I dati storici non vengono persi
- **Efficienza**: Operazioni mirate solo sui dati modificati
- **Scalabilità**: Adatto a grandi volumi di dati

---

**Tag**: `#ETL` `#DataPipeline` `#Database` `#DataEngineering` `#SQL`