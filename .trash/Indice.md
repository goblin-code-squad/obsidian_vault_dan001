
[[Data Analyst/Glossario/Flowchart]] 

[[Data Analyst/Glossario/Countif]] come funziona e come applicarlo
Per esempio cercando un singolo valore 
Countif colonna; valore; false

[[Data Analyst/Glossario/Vlookup]] cerca un valore in una tabella e ne restituisce un altro da un un altra colonna 

[[Data Analyst/Glossario/Variabili]] sono valori possibili 

[[Data Analyst/Glossario/Substitue]] per esempio da usare con gli accenti

[[Data Analyst/Glossario/Data catalog]] insieme strutturato di dati su cui lavorare con metadati e informazioni 

[[Data Analyst/Glossario/Tagging]] assegnazione di etichette a dataset o tabelle o colonne x classificazione 

[[Data Analyst/Glossario/And]] e [[Data Analyst/Glossario/OR]] [[Data Analyst/Glossario/operatori logici]]

frequenza assoluta e frequenza relativa e distribuzione frequenze 

[[Data Analyst/Glossario/Distribuzione Assoluta]]

[[Data Analyst/Glossario/Distribuzione Relativa]]

[[Data Analyst/Glossario/Data Visualisation]] 

### **[[Media]], [[Media]] E [[Moda]]**


#### **Definizioni**  
1. **Media (Aritmetica)**:  
   - La somma di tutti i valori divisa per il numero di osservazioni.  
   - **Formula**:  
     \[
    \text{Media} = \frac{\sum_{i=1}^{n} x_i}{n}
     \]  

2. **Mediana**:  
   - Il valore centrale in un dataset ordinato (se il numero di osservazioni è dispari).  
   - Se pari, la media dei due valori centrali.  

3. **Moda**:  
   - Il valore che compare più frequentemente nel dataset.  

---

### **Quando Usarle?**  
| **Misura** | **Vantaggi**                         | **Limitazioni**                     |  
|------------|--------------------------------------|-------------------------------------|  
| **Media**  | Usa tutti i dati.                    | Sensibile agli outlier.             |  
| **Mediana**| Robustà agli outlier.                | Ignora la distribuzione complessiva.|  
| **Moda**   | Utile per dati categorici.           | Può non esistere o non essere unica.|  

---

### **Esempi Pratici**  

#### **Dataset di Esempio**  
```python  
dati = [3, 7, 7, 8, 10, 13, 15]  
```  

#### **Calcoli**  
1. **Media**:  
   \[
   \frac{3 + 7 + 7 + 8 + 10 + 13 + 15}{7} = \frac{63}{7} = 9
   \]  

2. **Mediana**:  
   - Dataset ordinato: `[3, 7, 7, 8, 10, 13, 15]` → Valore centrale = **8**.  

3. **Moda**:  
   - Il numero **7** compare più volte (2 volte).  

---

### **Implementazione in Python**  
```python  
import statistics  

dati = [3, 7, 7, 8, 10, 13, 15]  

media = statistics.mean(dati)            # 9  
mediana = statistics.median(dati)        # 8  
moda = statistics.mode(dati)             # 7  
```  

---

### **Google Sheets**  
Usa le funzioni native:  
- **Media**: `=MEDIA(A1:A7)`  
- **Mediana**: `=MEDIANA(A1:A7)`  
- **Moda**: `=MODA(A1:A7)`  

---

### **Casi d’Uso**  
- **Media**: Calcolo del salario medio in un’azienda.  
- **Mediana**: Analisi del reddito per evitare distorsioni da outlier.  
- **Moda**: Identificare il prodotto più venduto.  

---

### **Domande Frequenti**  
❓ **Cosa scegliere se media e mediana sono diverse?**  
→ La mediana è più affidabile con outlier (es: redditi).  

❓ **E se tutti i valori sono unici?**  
→ La moda non esiste (dataset amodale).  

❓ **Come calcolare la media ponderata?**  
\[
\text{Media pesata} = \frac{\sum (x_i \cdot w_i)}{\sum w_i}
\]  
Esempio in Python:  
```python  
import numpy as np  
valori = [10, 20, 30]  
pesi = [0.5, 0.3, 0.2]  
media_ponderata = np.average(valori, weights=pesi)  
```  

---

**Nota**: Per distribuzioni multimodali, specificare tutte le mode (es: `statistics.multimode()` in Python).


