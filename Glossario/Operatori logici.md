### **AND e OR (Operatori Logici)**  

#### **Definizione**  
- **`AND`**: Operatore logico che restituisce `Vero` **solo se tutte le condizioni sono vere**.  
- **`OR`**: Operatore logico che restituisce `Vero` **se almeno una condizione è vera**.  

---

### **Dettagli**  
#### **1. Differenze Chiave**  
| Operatore | Esempio                     | Risultato (`A = Vero`, `B = Falso`) |  
|-----------|-----------------------------|--------------------------------------|  
| **AND**   | `A AND B`                   | `Falso` (perché B è falso)           |  
| **OR**    | `A OR B`                    | `Vero` (perché A è vero)             |  

#### **2. Priorità degli Operatori**  
- **`AND`** ha priorità maggiore di **`OR`** (a meno che non si usino parentesi).  
- Esempio:  
  ```  
  Condizione: (A OR B) AND C  
  Interpretazione: Prima si valuta `A OR B`, poi il risultato viene confrontato con `C`.  
  ```  

---

### **Esempi Pratici**  

#### **In Python**  
```python  
# Esempio con AND e OR  
x = 5  
print((x > 0) and (x < 10))  # True (entrambe vere)  
print((x > 10) or (x % 2 == 0))  # False (entrambe false)  
```  

#### **In SQL**  
```sql  
-- Filtra clienti con età > 30 E città = 'Roma'  
SELECT * FROM clienti WHERE età > 30 AND città = 'Roma';  

-- Filtra clienti con età < 20 O età > 60  
SELECT * FROM clienti WHERE età < 20 OR età > 60;  
```  

#### **In Excel/Google Sheets**  
```excel  
=IF(AND(A1 > 10, B1 = "Si"), "OK", "NO")  # Se A1 > 10 E B1 = "Si" → "OK"  
=IF(OR(A1 > 10, B1 = "Si"), "OK", "NO")   # Se A1 > 10 O B1 = "Si" → "OK"  
```  

---

### **Contesti d’Uso**  
- **Filtri**: Combinare condizioni in query SQL o DataFrame (Pandas).  
- **Validazione Dati**: Verificare più regole contemporaneamente (es: `IF (email LIKE "%@%") AND (len(password) >= 8)`).  
- **Machine Learning**: Definire regole complesse per feature engineering.  

---

### **Domande Tipiche**  
1. **"Come combinare più operatori AND/OR in una condizione?"**  
   ```python  
   # Python: Clienti con (età > 30 E città = "Roma") O (reddito > 50000)  
   condizione = (df["età"] > 30) & (df["città"] == "Roma") | (df["reddito"] > 50000)  
   ```  

2. **"Perché `AND` è valutato prima di `OR`?"**  
   *Risposta*: Per convenzione matematica (come in algebra). Usare parentesi per cambiare l’ordine.  

---

### **Best Practice**  
1. **Usare parentesi** per chiarire l’ordine di valutazione:  
   ```sql  
   -- Senza parentesi (confuso)  
   SELECT * FROM table WHERE A OR B AND C;  

   -- Con parentesi (chiaro)  
   SELECT * FROM table WHERE A OR (B AND C);  
   ```  

2. **Testare condizioni complesse** passo-passo per evitare errori.  

---

### **Errori Comuni**  
- Confondere **`AND`** con **`OR`**:  
  - `AND` richiede **tutte** le condizioni vere.  
  - `OR` richiede **almeno una** condizione vera.  
- Dimenticare le parentesi in espressioni complesse.  

---

Vuoi un esempio con **più di due condizioni** o un confronto con **XOR (OR esclusivo)**? 😊