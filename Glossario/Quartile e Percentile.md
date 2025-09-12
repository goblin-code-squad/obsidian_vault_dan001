### **[[Quartili]] e [[Percentili]] in Google Sheets: Guida Completa**

#### **📌 Differenze Chiave**
| **Metrica**    | **Cos'è**                                                 | **Divide i Dati in**                                    | **Esempio**                                 |
| -------------- | --------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------- |
| **Quartili**   | Valori che dividono i dati ordinati in **4 parti uguali** | 4 segmenti (Q0=min, Q1=25%, Q2=mediana, Q3=75%, Q4=max) | Q1 = Valore al 25° percentile               |
| **Percentili** | Valori che dividono i dati in **100 parti uguali**        | 100 segmenti (P1=1%, P50=mediana, P99=99%)              | P90 = Valore sotto cui cade il 90% dei dati |

---

### **📊 Formule Google Sheets**

#### **1. Per i QUARTILI (Q1, Q2, Q3)**
```excel
=QUARTILE(A2:A100, n)
```
- **n**:  
  - `0` = Valore minimo (Q0)  
  - `1` = Primo quartile (Q1, 25°)  
  - `2` = Mediana (Q2, 50°)  
  - `3` = Terzo quartile (Q3, 75°)  
  - `4` = Valore massimo (Q4)  

**Esempio**:  
```excel
=QUARTILE(A2:A100, 1)  // Restituisce Q1 (25° percentile)
```

---

#### **2. Per PERCENTILI Personalizzati (es: P10, P90)**
```excel
=PERCENTILE(A2:A100, k)
```
- **k**: Percentuale in decimale (es: 0.1 per P10, 0.9 per P90).  

**Esempio**:  
```excel
=PERCENTILE(A2:A100, 0.9)  // Restituisce P90
```

---

### **📌 Come Interpretarli**
- **Intervallo interquartile (IQR)**: Differenza tra Q3 e Q1 (`=Q3-Q1`).  
  - *Utile per identificare outlier*:  
    ```excel
    =Q1 - 1.5*IQR  // Limite inferiore
    =Q3 + 1.5*IQR  // Limite superiore
    ```
- **P90 > P50**: Distribuzione con coda a destra (più valori alti).  

---

### **📈 Esempio Pratico**
Supponiamo di avere i seguenti dati in **A2:A10**:  
`[10, 15, 20, 25, 30, 35, 40, 45, 50]`

| **Metrica** | **Formula**               | **Risultato** |  
|-------------|---------------------------|---------------|  
| Q1          | `=QUARTILE(A2:A10, 1)`    | 20            |  
| Mediana (Q2)| `=QUARTILE(A2:A10, 2)`    | 30            |  
| Q3          | `=QUARTILE(A2:A10, 3)`    | 40            |  
| P90         | `=PERCENTILE(A2:A10, 0.9)`| 46            |  

---

### **📌 Quando Usarli**
- **Quartili**: Per analisi rapide (es: ripartizione redditi).  
- **Percentili**: Per precisione (es: punteggi dei test, soglie di performance).  

---

### **⚠️ Attenzione**
- Google Sheets ignora automaticamente **celle vuote** e **testo**.  
- Per dati con **outlier**, la mediana (Q2) è più affidabile della media.  

---

### **💡 Extra: Box Plot in Google Sheets**
1. Seleziona i dati.  
2. **Inserisci > Grafico > Box plot**.  
3. Il grafico mostrerà:  
   - Minimo (Q0), Q1, Mediana (Q2), Q3, Massimo (Q4).  

Se hai bisogno di calcoli specifici per il tuo dataset, posso aiutarti! 😊
