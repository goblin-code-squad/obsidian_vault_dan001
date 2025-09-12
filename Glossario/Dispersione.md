### **📊 Cos'è la Dispersione Statistica?**  
La dispersione misura **quanto i dati si allontanano da un valore centrale** (come la media). Indica la "variabilità" di un dataset.  

---

### **📌 Perché è Importante?**  
- **Esempio**: Due classi hanno media 7 in matematica, ma:  
  - Classe A: voti tutti tra 6 e 8 → **Bassa dispersione** (omogenei)  
  - Classe B: voti da 3 a 10 → **Alta dispersione** (diversi tra loro)  

---

### **📈 Principali Misure di Dispersione**  

#### **1. Varianza**  
- **Formula**:  
  ```excel
  =VAR.P(A2:A100)  // Popolazione
  =VAR.C(A2:A100)  // Campione
  ```
- **Interpretazione**: Più è alta, più i dati sono "sparsi".  

#### **2. Deviazione Standard** (Radice quadrata della varianza)  
- **Formula**:  
  ```excel
  =DEV.ST.P(A2:A100)  // Popolazione
  =DEV.ST.C(A2:A100)  // Campione
  ```
- **Esempio**: Se la deviazione standard dei redditi è €15.000, i valori tipici distano €15.000 dalla media.  

#### **3. Intervallo Interquartile (IQR)**  
- **Formula**:  
  ```excel
  =QUARTILE(A2:A100, 3) - QUARTILE(A2:A100, 1)
  ```
- **Utile per**: Identificare outlier (valori anomali).  

#### **4. Range (Campo di Variazione)**  
- **Formula**:  
  ```excel
  =MAX(A2:A100) - MIN(A2:A100)
  ```
- **Limite**: Sensibile ai valori estremi.  

---

### **📊 Quando Usarle?**  
| **Scenario**              | **Misura Ideale**       |  
|---------------------------|-------------------------|  
| Dati simmetrici           | Deviazione standard     |  
| Presenza di outlier       | IQR                     |  
| Confronto tra gruppi      | Coefficiente di variazione (`=DEV.ST.C()/MEDIA()`) |  

---

### **📉 Esempio Pratico in Google Sheets**  
```excel
=ARRAYFORMULA({
  "Media"; MEDIA(B2:B100);
  "Dev. Std"; DEV.ST.C(B2:B100);
  "IQR"; QUARTILE(B2:B100, 3) - QUARTILE(B2:B100, 1)
})
```
**Output**:  
| Media | Dev. Std | IQR |  
|-------|----------|-----|  
| 75    | 12       | 20  |  

---

### **🔍 Interpretazione**  
- **Deviazione standard = 12**: Il 68% dei dati è tra 63 e 87 (media ± 1 dev.std).  
- **IQR = 20**: Il 50% centrale dei dati è distribuito in un intervallo di 20 punti.  

---

### **💡 Consigli**  
1. Usa **box plot** per visualizzare dispersione e outlier.  
2. Per confrontare gruppi con medie diverse, preferisci il **coefficiente di variazione**.  

Se vuoi analizzare un tuo dataset, posso aiutarti a calcolare queste metriche! 😊
