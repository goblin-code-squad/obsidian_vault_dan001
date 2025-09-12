Usare quasi sempre il grafico a barre

grafici a linea: usati se è solo se la linea  è il tempo

### **VISUALIZZAZIONE DEI DATI**  

#### **Definizione**  
La **visualizzazione dei dati** è la rappresentazione grafica di informazioni e dataset, progettata per comunicare pattern, trend e insight in modo chiaro ed efficace.  

---

### **Dettagli**  
#### **1. Tipi di Grafici e Loro Usi**  
| **Tipo di Grafico**       | **Scopo Principale**                          | **Esempio d’Uso**                     |  
|---------------------------|-----------------------------------------------|----------------------------------------|  
| **Bar Plot**              | Confronto tra categorie                       | Vendite per regione.                   |  
| **Line Plot**             | Trend temporali                               | Andamento stock nel tempo.             |  
| **Scatter Plot**          | Relazione tra due variabili numeriche         | Peso vs. Altezza.                      |  
| **Istogramma**            | Distribuzione di una variabile numerica       | Distribuzione di età in un campione.   |  
| **Box Plot**              | Visualizzare outliers e distribuzione         | Analisi performance dipendenti.        |  
| **Heatmap**               | Matrici di correlazione o dati geografici     | Correlazione tra feature in ML.        |  
| **Pie Chart**             | Composizione percentuale                      | Quote di mercato.                      |  

#### **2. Principi Fondamentali**  
- **Chiarezza**: Eliminare elementi non necessari (es: grid eccessivi).  
- **Accuratezza**: Scale degli assi proporzionali (evitare grafici fuorvianti).  
- **Contesto**: Aggiungere titoli, etichette e legende esplicative.  

---

### **Esempi Pratici**  

#### **1. Bar Plot (Python - Matplotlib/Seaborn)**  
```python  
import seaborn as sns  
import matplotlib.pyplot as plt  

data = {"Regione": ["Nord", "Centro", "Sud"], "Vendite": [120, 85, 65]}  
df = pd.DataFrame(data)  

sns.barplot(x="Regione", y="Vendite", data=df)  
plt.title("Vendite per Regione (2023)")  
plt.show()  
```  
**Output**: Un grafico a barre che confronta le vendite nelle tre regioni.  

#### **2. Line Plot per Trend Temporali**  
```python  
df = pd.DataFrame({  
    "Mese": ["Gen", "Feb", "Mar"],  
    "Utenti": [150, 320, 280]  
})  

sns.lineplot(x="Mese", y="Utenti", data=df, marker="o")  
plt.title("Utenti Attivi per Mese")  
plt.grid(True, linestyle="--")  
plt.show()  
```  

#### **3. Heatmap di Correlazione**  
```python  
corr_matrix = df.corr()  
sns.heatmap(corr_matrix, annot=True, cmap="coolwarm")  
plt.title("Matrice di Correlazione")  
plt.show()  
```  

---

### **Contesti d’Uso**  
- **Business Intelligence**: Dashboard per monitorare KPI.  
- **Data Science**: Esplorazione dati prima della modellazione.  
- **Comunicazione**: Report per stakeholder non tecnici.  

---

### **Domande Tipiche**  
1. **"Come scegliere il grafico giusto?"**  
   - Usa **barre** per confronti, **linee** per trend, **scatter** per relazioni.  
   - Evita i **pie chart** con troppe categorie (>5).  

2. **"Come migliorare l’estetica di un grafico?"**  
   ```python  
   sns.set_style("whitegrid")  # Sfondo grigliato  
   plt.xlabel("X Label", fontsize=12)  # Personalizza etichette  
   plt.xticks(rotation=45)  # Ruota etichette sull’asse X  
   ```  

---

### **Best Practice**  
1. **Strumenti Consigliati**:  
   - **Python**: Matplotlib, Seaborn, Plotly (interattivi).  
   - **BI**: Tableau, Power BI, Looker.  
2. **Accessibilità**:  
   - Usa colori contrastanti e pattern per daltonici.  
   - Aggiungi testo alternativo per grafici digitali.  

---

### **Esempio Avanzato (Plotly Interattivo)**  
```python  
import plotly.express as px  

fig = px.scatter(df, x="Peso", y="Altezza", color="Genere",  
                 title="Peso vs Altezza per Genere")  
fig.show()  
```  
**Vantaggio**: Tooltip interattivi e zoom.  

---

Vuoi un esempio di **dashboard completa** o come creare **mappe geografiche**? 😊

### **GRAFICI IN GOOGLE SHEETS**  

Google Sheets offre strumenti integrati per creare grafici in modo rapido e intuitivo. Ecco una guida completa con esempi pratici.  

---

## **1. Come Creare un Grafico**  
### **Passo-passo**  
1. **Seleziona i dati** (incluse le intestazioni di colonna/riga).  
2. Clicca su **Inserisci** → **Grafico**.  
3. Scegli il tipo di grafico dal menu a destra.  
4. Personalizza il grafico con le opzioni disponibili.  

---

## **2. Tipi di Grafici e Quando Usarli**  

| **Tipo di Grafico** | **Scopo** | **Esempio** |  
|---------------------|-----------|-------------|  
| **Grafico a colonne/barre** | Confronto tra categorie | Vendite per mese |  
| **Grafico a linee** | Trend nel tempo | Andamento stock |  
| **Grafico a torta** | Composizione percentuale | Quote di mercato |  
| **Grafico a dispersione (scatter)** | Relazione tra due variabili | Peso vs Altezza |  
| **Istogramma** | Distribuzione di frequenza | Distribuzione età |  
| **Grafico geografico** | Dati su mappe | Vendite per nazione |  

---

## **3. Esempi Pratici**  

### **Esempio 1: Grafico a Colonne (Vendite per Mese)**  
1. **Dati**:  
   | Mese   | Vendite |  
   |--------|---------|  
   | Gen    | 100     |  
   | Feb    | 150     |  
   | Mar    | 200     |  

2. **Procedura**:  
   - Seleziona i dati.  
   - Clicca su **Inserisci → Grafico**.  
   - Seleziona **"Grafico a colonne"**.  

   **Risultato**:  
   ![Grafico a colonne in Google Sheets](https://i.imgur.com/XYZ123.png)  

---

### **Esempio 2: Grafico a Linee (Trend Utenti)**  
1. **Dati**:  
   | Data       | Utenti |  
   |------------|--------|  
   | 01/01/2023 | 500    |  
   | 01/02/2023 | 800    |  
   | 01/03/2023 | 1200   |  

2. **Procedura**:  
   - Seleziona i dati.  
   - Clicca su **Inserisci → Grafico**.  
   - Seleziona **"Grafico a linee"**.  

   **Risultato**:  
   ![Grafico a linee in Google Sheets](https://i.imgur.com/ABC456.png)  

---

### **Esempio 3: Grafico a Torta (Distribuzione Categorie)**  
1. **Dati**:  
   | Categoria | % Mercato |  
   |-----------|-----------|  
   | Elettronica | 45%      |  
   | Abbigliamento | 30%    |  
   | Alimentari | 25%       |  

2. **Procedura**:  
   - Seleziona i dati.  
   - Clicca su **Inserisci → Grafico**.  
   - Seleziona **"Grafico a torta"**.  

   **Risultato**:  
   ![Grafico a torta in Google Sheets](https://i.imgur.com/DEF789.png)  

---

## **4. Personalizzazione Avanzata**  
Google Sheets permette di modificare:  
✅ **Titolo e legenda**  
✅ **Colori e stile**  
✅ **Assi (min/max, scala logaritmica)**  
✅ **Etichette dati (valori sulle barre/linee)**  

**Esempio**:  
```  
1. Clicca sul grafico → "Personalizza" nel menu a destra.  
2. Modifica titolo, colori o aggiungi etichette.  
```  

---

## **5. Grafici Dinamici (con Filtri)**  
Se i dati cambiano, il grafico si aggiorna automaticamente!  

**Esempio**:  
- Aggiungi un filtro (**Dati → Filtro**).  
- Seleziona un intervallo diverso e il grafico si adatterà.  

---

## **6. Esportazione e Condivisione**  
- **Download** come PNG/PDF:  
  ```  
  Clicca sul grafico → ⋮ (menu) → "Scarica come" → PNG/PDF.  
  ```  
- **Incorpora** in Google Sites/Docs:  
  ```  
  Copia e incolla direttamente.  
  ```  

---

## **Domande Frequenti**  
❓ **Come aggiungere una seconda serie di dati?**  
→ Seleziona i dati aggiuntivi e trascinali nell’editor grafico.  

❓ **Come cambiare il tipo di grafico dopo averlo creato?**  
→ Clicca sul grafico → Menu a destra → "Tipo di grafico".  

❓ **Come creare un grafico combinato (es: barre + linee)?**  
→ Usa l’opzione **"Grafico combinato"** e imposta serie diverse.  

---

### **Conclusione**  
Google Sheets rende semplice creare grafici professionali in pochi clic, con aggiornamenti automatici e opzioni di personalizzazione.  

**Vuoi un esempio passo-passo per un grafico specifico?** 😊