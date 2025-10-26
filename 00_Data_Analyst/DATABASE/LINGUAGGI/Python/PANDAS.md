2025_10_17

Pandas

Cos'e' un Dataframe

- Rappresentazione di una tabella
- Possiamo generarlo attraverso:

e' un Json dove 

- la chiave è il nome della colonna
- Il valore è l’array degli elementi della colonne
- Lettura da sorgenti varie: per ora abbiamo visto csv
[https://pandas.pydata.org/docs/getting_started/intro_tutorials/08_combine_dataframes.html](https://pandas.pydata.org/docs/getting_started/intro_tutorials/08_combine_dataframes.html)

  Per combinare dei dati:

- Concat ([Merging concat](https://pandas.pydata.org/docs/user_guide/merging.html#merging-concat))
- Merge ([pandas.merge(...)](https://pandas.pydata.org/docs/reference/api/pandas.merge.html#pandas.merge) , [Merging join](https://pandas.pydata.org/docs/user_guide/merging.html#merging-join))

ATTENZIONE:
[Confronto tra pandas e SQL](https://pandas.pydata.org/docs/getting_started/comparison/comparison_with_sql.html#compare-with-sql-join)
  
- Filtri
- Is_null
- Unique

- Parsing/pre-processing
    
- Pivot
    

  

- Scrittura dei dati su db
    

  

## PARKING LOT

- Funzione reset_index
    

- [Reset index](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html)
    
- [Multi index](https://pandas.pydata.org/docs/user_guide/advanced.html#advanced)

un [[dataframe]] di pandas e' una struttura dati che puo' esser eun array o una tabella (qui c'e' un esmepio che ha la struttura di un jason particolare)
```json

import pandas as pd  
  
data = {  
  "calories": [420, 380, 390],  
  "duration": [50, 40, 45]  
}  
  
#load data into a DataFrame object:  
df = pd.DataFrame(data)  
  
print(df)
```

da qui in poi abbiamo seguito pari passo
questo tutorial (il solito che usiamo)
e Teresa ci ha commentato le cose

https://pandas.pydata.org/docs/getting_started/intro_tutorials/08_combine_dataframes.html

comparazione tra SQL Join e Pandas Merge
(questa e' una riechiesta comune in classe)

https://pandas.pydata.org/docs/getting_started/comparison/comparison_with_sql.html#compare-with-sql-join


e' possibile importare anche matplotlib e pandas in automatico puo' creare un grafico con i dati gia' da solo facendo nome_dataframe.plot9()

prende in automatico dei dati quindi non puo' essere perfetto ma e' comodo per vedre un grafico di una tabella on the fly



29 09 2025 - 
PANDAS

Dopo il lavoro in minin gruppi su come imparare ad usare Pandas in cui abbiamo condiviso una serie di informazioni su Drive [https://docs.google.com/document/d/1abCK5QB54glAeDa2ljb3UYy7Ysqx0fMSpcyzFYm9ePQ/edit?usp=sharing](https://docs.google.com/document/d/1abCK5QB54glAeDa2ljb3UYy7Ysqx0fMSpcyzFYm9ePQ/edit?usp=sharing)

 siamo andati su Jupyter facendo jupyter notebook da VISUAL STUDIO CODE e poi abbiamo recuperato l'indirizzo da Slack: [https://dati.mit.gov.it/catalog/dataset/opere-incompiut](https://dati.mit.gov.it/catalog/dataset/opere-incompiut)

e in cui abbiamo un db di opere incompiute.

  

Installiamo Jupyter  creando dentro Jupiter un nuovo file con +New in alto a destra

Dentro VSD salgo di una cartella col comando cd .. (cd spazio punto punto - cd = "change directory")

Dentro File System CTRL DX dentro VSC vedo un file nuovo da Notebook 

  

Per analizzare il file ci servono: 

1. il file possibilmente dentro la stessa cartella

2. il csv dopo l'import di pandas 

3. le istruzioni: non sappiamo ancora come leggere un file .csv con pandas per cui chiediamo alla documentazione ufficiale su google ad esempio con "read csv with pandas" >>> pd.read_csv ('data.csv')

  

import pandas as pd

pd.read_csv('opereincompiute2016.csv')

  

--> Il terminale si comporta come una REPL - READ - EXECUTE - PRINT - LOOP

  

pd.read_csv su VSC restituisce il db

il DATAFRAME lo possiamo mettere dentro una variabile

con df=pd.read_csv('opereincompiute2016.csv')

e poi richiamo df

  

poi vado a cercare come selezionare ad es. tutti i CODICI FISCALI --> cerco in documentazione

def

  come fare il fitrlo di un dataframe nel mondo pandas
```python
import pandas as pd 
data = 
df=pd.DataFrame(data)
```


```python
df['filtro']
```

dove df e' una condizione di filtro
questo permette di filtrare il dataframe in modo assurdi tipo con i risultati delle api 

##
FUNZIONi viste

pandas.DataFrame.sort_index

pandas.concat([objects], parametri)

pandas.sort_values("colonna")

[[Pandas_MERGE]]

air_quality = pd.merge(air_quality, stations_coord, how="left", on="location")
air_quality.head()