### **VARIABILI DICOTOMICHE, QUANTITATIVE E QUALITATIVE**  

#### **1. Variabili Dicotomiche (o Binarie)**  
**Definizione**: Variabili con **solo due valori possibili**, spesso rappresentate come `0/1`, `Vero/Falso`, o `Sì/No`.  
**Esempi**:  
- `Sesso` (M/F) → Codificata come `0` e `1`.  
- `Ha_credito` (Sì/No).  
**Caratteristiche**:  
- Sottocaso di variabili **categoriche nominali**.  
- Usate in modelli statistici (es: regressione logistica).  
**Esempio in Python**:  
```python  
df["Ha_credito"] = df["Ha_credito"].map({"Sì": 1, "No": 0})  # Conversione a binario  
```  

---

#### **2. Variabili Quantitative**  
**Definizione**: Variabili **numeriche**, misurabili su una scala.  
**Sottotipi**:  
- **Continue**: Valori qualsiasi in un intervallo (es: `Peso`, `Temperatura`).  
- **Discrete**: Valori interi (es: `Numero_figli`, `Conteggio_ordini`).  
**Esempi**:  
- `Età`: 25, 30, 42 (discreta se intera, continua se decimale).  
- `Reddito_annuale`: 35000.50 € (continua).  
**Uso**:  
- Analisi statistica (media, deviazione standard).  
- Feature per modelli ML (normalizzazione spesso richiesta).  
**Esempio in Python**:  
```python  
df["Reddito_normalizzato"] = (df["Reddito"] - df["Reddito"].mean()) / df["Reddito"].std()  
```  

---

#### **3. Variabili Qualitative (o Categoriche)**  
**Definizione**: Variabili che rappresentano **categorie o gruppi**, non numeriche.  
**Sottotipi**:  
- **Nominali**: Senza ordine (es: `Colore` ["Rosso", "Verde"]).  
- **Ordinali**: Con ordine (es: `Livello_istruzione` ["Medio", "Laurea", "PhD"]).  
**Esempi**:  
- `Città`: ["Roma", "Milano"] (nominale).  
- `Soddisfazione`: ["Basso", "Medio", "Alto"] (ordinale).  
**Uso**:  
- Devono essere codificate per l'analisi (es: one-hot encoding per nominali).  
**Esempio in Python**:  
```python  
# One-hot encoding per variabili nominali  
df_encoded = pd.get_dummies(df, columns=["Città"])  
```  

---

### **CONFRONTO CHIAVE**  
| **Tipo**          | **Esempio**            | **Scala**      | **Trattamento Tipico**        |  
|--------------------|------------------------|----------------|-------------------------------|  
| **Dicotomica**     | Sì/No                  | Binaria        | Codifica 0/1                  |  
| **Quantitativa**   | Età, Reddito           | Numerica       | Normalizzazione               |  
| **Qualitativa**    | Colore, Livello        | Categorica     | One-hot encoding (nominali)   |  

---

### **Contesti d’Uso**  
- **Machine Learning**:  
  - Le variabili **quantitative** sono spesso normalizzate.  
  - Le variabili **qualitative** richiedono codifica (es: `LabelEncoder` per ordinali).  
- **Statistica Descrittiva**:  
  - Le variabili **dicotomiche** sono analizzate con frequenze relative.  
  - Le variabili **ordinali** usano mediane (non medie!).  

---

### **Domande Tipiche**  
1. **Perché codificare le variabili qualitative?**  
   *Risposta*: Perché i modelli matematici lavorano con numeri, non testo (es: "Rosso" → [1, 0, 0] con one-hot).  

2. **Quando usare la mediana invece della media?**  
   *Risposta*: Per variabili **ordinali** o quantitative con **outlier** (es: redditi).  

3. **Come gestire una variabile come "CAP" (alta cardinalità)?**  
   *Risposta*: Raggruppare per aree geografiche o usare tecniche di embedding.  

---

### **Esempio Integrato**  
```python  
# Dataset di esempio  
data = {  
    "Età": [25, 30, 35],                     # Quantitativa discreta  
    "Sesso": ["M", "F", "M"],                 # Dicotomica (se binaria)  
    "Livello": ["Basso", "Medio", "Alto"]     # Qualitativa ordinale  
}  
df = pd.DataFrame(data)  

# Codifica  
df["Sesso"] = df["Sesso"].map({"M": 1, "F": 0})            # A binario  
df["Livello"] = df["Livello"].map({"Basso": 0, "Medio": 1, "Alto": 2})  # Ordinale a numerico  
```  

**Output**:  
| Età | Sesso | Livello |  
|-----|-------|---------|  
| 25  | 1     | 0       |  
| 30  | 0     | 1       |  
| 35  | 1     | 2       |  

---

**Best Practice**:  
- Documentare sempre il **tipo** e la **scala** di ogni variabile.  
- Verificare la **distribuzione** prima di scegliere la codifica.  

Vuoi un esempio di **analisi esplorativa** con mix di variabili? 😊