### **VLOOKUP**  

#### **Definizione**  
**VLOOKUP** (Vertical Lookup) è una funzione utilizzata in **Excel** e altri strumenti (come Google Sheets) per cercare un valore in una colonna specifica di una tabella e restituire un corrispondente valore da un'altra colonna.  

---

### **Sintassi Base**  
```excel
=VLOOKUP(valore_da_cercare, tabella_di_riferimento, indice_colonna, [tipo_di_ricerca])
```  
- **`valore_da_cercare`**: Il valore da trovare nella prima colonna della tabella.  
- **`tabella_di_riferimento`**: L'intervallo di celle che contiene i dati.  
- **`indice_colonna`**: Il numero della colonna (nella tabella) da cui restituire il valore.  
- **`[tipo_di_ricerca]`**:  
  - **`FALSE`** (o `0`): Ricerca **esatta**.  
  - **`TRUE`** (o `1`): Ricerca **approssimata** (richiede ordinamento crescente).  

---

### **Esempio Pratico in Excel**  
Supponiamo di avere due tabelle:  

1. **Tabella Prodotti** (dove cercare):  
   | **ID** | **Prodotto** | **Prezzo** |  
   |--------|-------------|----------|  
   | 101    | Laptop      | 999      |  
   | 102    | Smartphone  | 599      |  

2. **Tabella Ordini** (dove inserire la formula):  
   | **ID_Ordine** | **ID_Prodotto** | **Prodotto** (da popolare) | **Prezzo** (da popolare) |  
   |--------------|----------------|--------------------------|------------------------|  
   | 1            | 102            | =VLOOKUP(B2, A1:C3, 2, FALSE) → "Smartphone" | =VLOOKUP(B2, A1:C3, 3, FALSE) → 599 |  

**Risultato**:  
- La formula cerca `102` nella prima colonna della tabella prodotti e restituisce:  
  - Nome prodotto dalla colonna 2.  
  - Prezzo dalla colonna 3.  

---

### **Limitazioni e Alternative**  
1. **Problemi Comuni**:  
   - **La colonna di ricerca deve essere la prima** nella tabella di riferimento.  
   - **Non cerca a sinistra**: Se il valore da restituire è a sinistra del criterio, usare **INDEX/MATCH** o **XLOOKUP** (in Excel 365).  

2. **Alternativa Migliore (XLOOKUP)**:  
   ```excel
   =XLOOKUP(valore_da_cercare, colonna_di_ricerca, colonna_di_risultato, [se_non_trovato], [modalità_ricerca])
   ```  
   - Più flessibile (cerca in qualsiasi direzione).  

---

### **Contesti d’Uso**  
- **Excel/Google Sheets**: Unire dati da tabelle diverse (es: da un foglio "Prodotti" a un foglio "Ordini").  
- **ETL**: Strumenti come Power Query replicano questa logica per integrare dati.  
- **Database**: Equivalente a un **LEFT JOIN** in SQL.  

---

### **Domanda Tipica**  
*"Perché VLOOKUP restituisce #N/A?"*  
**Cause comuni**:  
1. Il valore cercato non esiste (usare `=SEERRORE(VLOOKUP(...); "Valore non trovato")`).  
2. La colonna di ricerca non è la prima nella tabella.  
3. La modalità di ricerca è `FALSE` ma i dati non sono esatti.  

---

### **Esempio con Dati Reali**  
```excel
# Trova il dipartimento di un impiegato
=VLOOKUP("Mario Rossi", A2:B100, 2, FALSE)
```  
- Cerca "Mario Rossi" nella colonna `A` e restituisce il dipartimento dalla colonna `B`.  

---

**Best Practice**:  
- Usare **nomi di intervallo** (es: `=VLOOKUP(B2, TabellaProdotti, 3, FALSE)`) per formule più leggibili.  
- Preferire **XLOOKUP** o **INDEX/MATCH** per maggiore flessibilità.  

Vuoi un esempio di **VLOOKUP con più criteri** o l'equivalente in Python? 😊