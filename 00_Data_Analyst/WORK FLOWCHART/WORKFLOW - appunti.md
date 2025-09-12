PARTENDO DALLE DIMENSIONI FOGLIA DEL MODELLO DIMENSIONALE E TROVANDO LA/LE TABELLE RELATIVE SU LANDING
PER OGNI TABELLA

    PRENDERE LA TABELLA DA LANDING
    
    PULIZIA DATI CON CHECK DI QUALITÁ (ES. DATE SENSATE, NESSUNA INCONSISTENZA TRA I DATI)
    
    1a. CONTROLLO SE C'É UNA CHIAVE DUPLICATA
        PER LE RIGHE CON CHIAVE DUPLICATA NE PRENDO UNA
        
    1b. CREO TABELLA CON RIGHE NON DUPLICATE IN INTEGRATION LAYER 
    2a. CONTROLLO SE CI SONO DELLE CHIAVI ESTERNE ROTTE (RIFERIMENTO CHE NON ESISTE) 
    PER LE RIGHE CON RIFERIMENTI CHE NON ESISTONO DENTRO LE TABELLE REFERENZIATE CREO DEI FITTIZZI A CUI COLLEGO I DATI
    2b. CREO TABELLA CON RIGHE CON RIFERIMENTI DELLE CHIAVI CORRETTE UNITE ALLE RIGHE CON RIFERIMENTI ERRATI CORRETTI PUNTANDO AI FITTIZZI





1. controllo che la chiave non sia duplicata
2. controllo che la chiave non sia null
3. controllo foreign key complete FK (che ogni figlio abbia un padre cioe' vado in leftjoin e verifico quando la connessione e' null
   p.e. vado in left dal figlio al padre e trovo chi e' orfano 
   select * from figlio.* LEFT JOIN
   ON figlio.* = padre.*
   where id_padre is null
   faccio il controllo ID padre

```sql
join where il padre e' null
```


La unique e' fondamentale perche' mi serve per evitare un double counting

ora inseriamo in customer andiamo ad aggiungere un fittizio per ogni country (i dati che ci macano e che ricostruiamo con invoice_id)

poi fare una query che inserisce N numeri di cose

facciamo una union dei country e gli diamo una chiave

key esterna un customer_country