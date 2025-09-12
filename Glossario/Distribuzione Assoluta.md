CountIf

### **DISTRIBUZIONE ASSOLUTA**  

#### **Definizione**  
La **distribuzione assoluta** (o *frequenza assoluta*) è il conteggio del numero di volte in cui un valore o una categoria si presenta in un dataset.  

---

### **Dettagli**  
#### **1. Caratteristiche**  
- **Sempre un numero intero** ≥ 0.  
- **Non normalizzata**: Dipende dalla dimensione del campione.  
- **Usata per dati discreti o categorici** (es: conteggio di prodotti venduti per categoria).  

#### **2. Formula**  
Per una categoria \( x \):  
\[
\text{Frequenza Assoluta}(x) = \text{Numero di osservazioni con valore } x
\]  

---

### **Esempi Pratici**  

#### **Esempio 1: Conteggio Categorie (Python - Pandas)**  
```python  
import pandas as pd  

# Dataset di esempio  
df = pd.DataFrame({"Colore": ["Rosso", "Blu", "Rosso", "Verde", "Blu", "Blu"]})  

# Calcolo distribuzione assoluta  
distribuzione_assoluta = df["Colore"].value_counts()  
print(distribuzione_assoluta)  
```  
**Output**:  
```  
Blu     3  
Rosso   2  
Verde   1  
```  

#### **Esempio 2: Dati Discreti (Excel)**  
| **Voto** | **Frequenza Assoluta** |  
|----------|------------------------|  
| 18       | 5                      |  
| 22       | 12                     |  
| 30L      | 3                      |  

---

### **Contesti d’Uso**  
1. **Analisi Esplorativa**:  
   - Capire quanto è frequente una categoria (es: prodotti più venduti).  
2. **Controllo Qualità**:  
   - Identificare valori anomali (es: una categoria con conteggio insolitamente basso).  
3. **Preparazione Grafici**:  
   - Creare istogrammi o bar plot (es: `sns.countplot` in Seaborn).  

---

### **Confronto con Frequenza Relativa**  
| **Metrica**           | **Formula**                          | **Esempio (Blu: 3 su 6)** |  
|------------------------|--------------------------------------|---------------------------|  
| **Frequenza Assoluta** | Conteggio grezzo                     | 3                         |  
| **Frequenza Relativa** | \( \frac{\text{Freq. Assoluta}}{N} \) | \( \frac{3}{6} = 0.5 \)   |  

---

### **Domande Tipiche**  
1. **"Quando usare la frequenza assoluta invece di quella relativa?"**  
   *Risposta*:  
   - Usa l’**assoluta** per conteggi concreti (es: "10 clienti hanno scelto l'opzione A").  
   - Usa la **relativa** per confrontare gruppi di dimensioni diverse (es: "Il 20% dei clienti preferisce A").  

2. **"Come calcolare la frequenza assoluta in SQL?"**  
   ```sql  
   SELECT Colore, COUNT(*) AS Frequenza_Abs  
   FROM Prodotti  
   GROUP BY Colore;  
   ```  

---

### **Best Practice**  
- **Visualizzazione**: Accompagnare sempre i conteggi assoluti con grafici a barre per chiarezza.  
- **Limitazioni**: Non confrontare direttamente frequenze assolute tra dataset di dimensioni diverse.  

**Strumenti**:  
- Python: `collections.Counter`, `pandas.Series.value_counts()`.  
- R: `table()`.  

---

Vuoi un esempio di **istogramma con frequenze assolute** o come calcolarle per **dati raggruppati**? 😊