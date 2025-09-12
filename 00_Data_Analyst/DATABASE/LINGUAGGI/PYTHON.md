print(hello)

print e' funzione
hello e' argomento

qualcosa=2 qualcosa e' una variabile

snakecase: convenzione per python di scrivere_tutto_attaccato

In Python, una **chiamata di funzione** (function call) è l'esecuzione di un blocco di codice riutilizzabile definito in precedenza con `def`.  

### Come funziona:
1. **Dichiari** la funzione (una volta).  
2. **La chiami** (quante volte vuoi) per eseguirla.  

---

### 📌 **Esempio Base**
```python
# 1. DEFINIZIONE
def saluta(nome):
    print(f"Ciao, {nome}!")

# 2. CHIAMATA
saluta("Mario")  # Output: Ciao, Mario!
```
- **`saluta`** è il nome della funzione.  
- **`"Mario"`** è l'argomento (input) passato alla funzione.  

---

### 🔹 **Cosa succede quando chiami una funzione?**
1. Python "salta" al corpo della funzione (blocco sotto `def`).  
2. Esegue il codice **usando gli argomenti forniti**.  
3. **Torna** al punto dove è stata chiamata (eventualmente restituendo un valore con `return`).  

---

### 📚 **Tipi comuni di chiamate**
1. **Senza argomenti**:  
   ```python
   def dice_ciao():
       print("Ciao!")
   
   dice_ciao()  # Chiamata
   ```

2. **Con argomenti posizionali**:  
   ```python
   def somma(a, b):
       return a + b
   
   risultato = somma(3, 5)  # 8
   ```

3. **Con argomenti nominati (keyword arguments)**:  
   ```python
   def info(nome, età):
       print(f"{nome} ha {età} anni.")
   
   info(età=30, nome="Alice")  # Ordine diverso
   ```

4. **Funzioni built-in**: Anche quelle di Python sono chiamate così:  
   ```python
   len("hello")  # 5
   int("42")     # 42
   ```

---

### ⚠️ **Attenzione!**
- Se chiami una funzione **senza `()`**, non la esegui:  
  ```python
  print(saluta)  # Stampa l'oggetto funzione, non esegue il codice!
  ```

---

### 💡 **Perché usare le funzioni?**
- **Riutilizzo**: Scrivi una volta, usa ovunque.  
- **Modularità**: Spezzi il codice in parti logiche.  
- **Debugging**: Più facile testare pezzi isolati.  

Esempio con `return`:  
```python
def quadrato(n):
    return n * n

x = quadrato(4)  # x ora è 16
``` 

Se hai dubbi su casi specifici, chiedi pure! 🚀

\r
\r\n

per andare gli a capo si usano questi caratteri invisibili negli editor
in linux si usa \n e in windows \r 
gli a capo sono importanti

se lancio piu' volte fetchall (che prende tutta la roba)
se glielo chiedo la seconda volta non mi ritorna niente perche' ha gia' letto tutto
quindi basta usare print per vederlo

```python
def sum(a,b):
	return a+b
```

def chiama una fuzione
sum e' la funzione
a b i parametri
la definizioe e' dopo tutto quello che e' tabulato a destra
	con indentatione

attenzione
= significa assegnare un valore a qualcosa
== invece significa somma 

le parenetesi quadre racchiudono un array 
le parentesi tonde con virgola racchiudono una tupla

una tupla e' una riga un array una serie di array (circa)
ogni elemento nella tupla e' una colonna

[( 0 0 0 0 ),
( 0 0 0 0 ),
( 0 0 0 0 )]

[[ARRAY]]

tupla 

cursore

funzione

modulo

definire una variabile e' salvare quella variabile, serve per dire al programma cosa sia e fargliela memorizzare visto che gli diamo un valore