
| **Metrica**  | **Cos'è**                                                 | **Divide i Dati in**                                    | **Esempio**                   |
| ------------ | --------------------------------------------------------- | ------------------------------------------------------- | ----------------------------- |
| **Quartili** | Valori che dividono i dati ordinati in **4 parti uguali** | 4 segmenti (Q0=min, Q1=25%, Q2=mediana, Q3=75%, Q4=max) | Q1 = Valore al 25° percentile |

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
