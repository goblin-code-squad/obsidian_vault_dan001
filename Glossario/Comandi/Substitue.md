### **SUBSTITUTE (Excel/Google Sheets)**  

#### **Definizione**  
**SUBSTITUTE** è una funzione in Excel/Google Sheets che **sostituisce un testo specifico con un altro** all'interno di una stringa. È utile per correggere errori, standardizzare formati o pulire dati testuali.  

---

### **Sintassi**  
```excel
=SUBSTITUTE(testo_originale, testo_vecchio, testo_nuovo, [istanza_num])
```  
- **`testo_originale`**: La stringa in cui cercare.  
- **`testo_vecchio`**: Il testo da sostituire.  
- **`testo_nuovo`**: Il nuovo testo da inserire.  
- **`[istanza_num]`** (opzionale): Specifica quale occorrenza sostituire (se omesso, sostituisce tutte).  

---

### **Esempi Pratici**  

#### **1. Sostituzione Semplice**  
```excel
=SUBSTITUTE("Ciao mondo", "mondo", "universo")  
```  
**Risultato**: `"Ciao universo"`  

#### **2. Sostituzione di un Carattere Specifico**  
```excel
=SUBSTITUTE("123-456-789", "-", "")  # Rimuove tutti i "-"  
```  
**Risultato**: `"123456789"`  

#### **3. Sostituzione della Terza Occorrenza**  
```excel
=SUBSTITUTE("A-B-C-D-E", "-", " ", 3)  
```  
**Risultato**: `"A-B-C D-E"` (solo il terzo `"-"` è sostituito con uno spazio).  

---

### **Confronto con REPLACE**  
| Funzione      | Scopo                                     | Esempio                          |  
|--------------|------------------------------------------|----------------------------------|  
| **SUBSTITUTE** | Sostituisce **testo** (senza posizione fissa) | `=SUBSTITUTE("A1B1", "1", "2")` → `"A2B2"` |  
| **REPLACE**    | Sostituisce **per posizione** (es: caratteri 2-3) | `=REPLACE("ABCD", 2, 2, "X")` → `"AXD"` |  

---

### **Contesti d’Uso**  
1. **Pulizia Dati**:  
   - Correggere errori di battitura (`"Gogle"` → `"Google"`).  
   - Standardizzare formati (`"01/02/2023"` → `"01-02-2023"`).  

2. **Preparazione per Analisi**:  
   - Rimuovere caratteri indesiderati (spazi extra, simboli).  

3. **Costruzione di Stringhe Dinamiche**:  
   ```excel
   =SUBSTITUTE("Il cliente [Nome] ha speso [Importo]", "[Nome]", "Mario")  
   ```  

---

### **Domande Tipiche**  
1. **Come sostituire solo la prima occorrenza?**  
   ```excel
   =SUBSTITUTE("A-B-C-D", "-", " ", 1)  # Risultato: "A B-C-D"  
   ```  

2. **Come usare SUBSTITUTE con altre funzioni?**  
   Esempio: Estrai il testo dopo l'ultimo "/":  
   ```excel
   =RIGHT(A1, LEN(A1) - FIND("§", SUBSTITUTE(A1, "/", "§", LEN(A1)-LEN(SUBSTITUTE(A1, "/", "")))))  
   ```  

---

### **Alternativa in Python**  
In Python, usa `.replace()` o `re.sub()`:  
```python
text = "Ciao mondo"
new_text = text.replace("mondo", "universo")  # "Ciao universo"
```  

---

**Best Practice**:  
- Usare **SUBSTITUTE** per sostituzioni basate su contenuto, **REPLACE** per posizioni fisse.  
- Combinare con **TRIM** per rimuovere spazi extra:  
  ```excel
  =TRIM(SUBSTITUTE(A1, "  ", " "))  # Sostituisce doppi spazi con singoli
  ```  

Vuoi un esempio avanzato (es: sostituire più valori in una formula)? 😊