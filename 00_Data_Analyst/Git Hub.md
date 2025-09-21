# **commit** : salva localmente
Salva le modifiche fatte ai file nel repository locale. Non invia nulla al server remoto.

# **fetch** = scarica aggiornamenti
Scarica gli aggiornamenti dal repository remoto, ma non li applica automaticamente al tuo lavoro locale.

# pull = scarica e aggiorna
git pull: Scarica gli aggiornamenti dal repository remoto e li applica subito al tuo lavoro locale (fa fetch + merge).
	**MERGE** = Il **merge** in Git è un’operazione che unisce le modifiche di due branch diversi in uno solo.  Quando fai un merge, Git integra i commit di un branch (ad esempio `feature`) dentro un altro (ad esempio `main`), creando un nuovo commit di “fusione”.
	**REBASE** = è un’operazione che permette di spostare o combinare una sequenza di commit su una nuova base. Serve per “riscrivere” la cronologia, rendendola più lineare e pulita, ad esempio applicando le modifiche di un branch sopra un altro.
	**CHERRY PICK** = Il comando cherry-pick in Git serve per applicare un singolo commit da un branch a un altro, senza unire tutti i commit come nel merge o rebase.
# push = invia 
serve per inviare  le modifiche che hai salvato, in modo che tutt3 possano vedere le tue modifiche


- **Staged** (indicizzati): sono i file che hai aggiunto all’area di staging con `git add` e che saranno inclusi nel prossimo commit.
- **Unstaged** (non indicizzati): sono le modifiche apportate ai file che non sono ancora state aggiunte all’area di staging, quindi non verranno incluse nel commit finché non usi `git add`.

**In sintesi:**

- Modifiche unstaged = non pronte per il commit
- Modifiche staged = pronte per il commit

TEMA SU GITHUB: iniziamo a pensare alla GESTIONE DEL CONFLITTO

Per avere in locale PARKING LOT che è un repository che sappiamo esistere dobbiamo clonarlo.

Uso CLONE in git che scarica i file e crea collegamenti tra i file in locale e quello che c’è in remoto.

La magia di FETCH è che restituisce le modifiche che sono state fatte.

Modifiche online che non abbiamo scaricato in locale. Non aggiorno la posizione della MAIN.

BRANCH è un **ramo delle repository**.

Che cosa è una BRANCH? E’ legato al concetto di MAIN, sono la stessa cosa ma una è in locale e una in remoto, sono delle etichette che punto a dei commit. Le **BRANCH** sono dei **puntatori che puntano dei commit**, che sono insiemi di versioni dei nostri file/modifiche /aggiornamenti/cancellamenti. Aggiungendoli gli uni sugli altri abbiamo una storia.

  
  ---
  

MAIN dice cosa vede Marco in locale. _**La PULL sposta l’etichetta MAIN in ORIGIN/MAIN**_ e vede tutti i comandi nel mezzo.

Quando iniziamo a lavorare facciamo un PULL delle modiche. Se faccio FETCH non ho l’ultimo dato del codice.

Lavoro sempre sulla stessa cartella a prescindere dagli strumenti che uso.

  
  

GIT fa in modo di passare in un file da una versione A ad una versione B e ti fa vedere come cambiare le cose.

  
  

PULL ha due configurazioni che sono:

1. MERGE
    
2. REBASE
    

Il conflitto può apparire in parti vicine della stessa linea.

  
  

PULL: unire le cose che ho fatto io e quello che han fatto gli altri e le metto insieme.

Le versioni 1 e 2 cambiano le forme dell’albero che è lo schema.

Branchin models  DA CERCARE SUL WEB

  

_11/09/2025 POMERIGGIO_

    

Import = funzione

Estrazione_vincitori = modulo (un modulo è un insieme di funzioni)

IL modulo lo importo.

MODULO.FUNZIONE

  
_**Con = sqlite3.connect(“membri_dan001”)**_

Con è una variabile e a destra dell’= c’è il valore della variabile.

Con la funzione **connect** ci colleghiamo ad un database per farci sopra delle operazioni oppure posso andare ad eseguire dei parametri che sono dentro le parentesi.

Le funzioni possono ritornare qualcosa (return) oppure no (in tal caso ha dei side effect che sono funzionali)

Il modulo risolve tutte le problematiche che qualcuno ha già incontrato e che possiamo eseguire (perciò se lo vado a cercare nella documentazione molto probabilmente lo troverò.

Andando dentro l’editor di VSC sopra alle funzioni esce una definizione e delle info. Dopo l’invio nel terminale ho l’effetto della funzione.


(Non mi devo ricordare tutto ma imparare a ragionare sul problema che ho.)

**Sequenze:**

1. CONNETTERSI
    
2. Usare il CURSORE
    
3. Fetchall restituisce una lista di TUPLE
    
4. OGNI TUPLA rappresenta una riga di output dentro parentesi tonde
    
5. Una stringa è tra due “”, senza viene letto come una variabile
    

  
  

_**Cur = con.cursor()**_

  
  

**fortunati_analyst= ["Alessandro Alvisi","Alessia Urru","Alessio Pedrotti","Alice Innoc…**

fortunati_analyst è la variabile definita con l’= e ciò che segue è una lista, che riconosco perché è definita dalle [] con all’interno delle stringhe che sono tra “”, se fossero delle tuple sarebbero invece tra () con dentro la virgola.

  
  

  
  

  
  

**Passare da una stringa ad una tupla:**

con le liste interagiamo scrivendo **lista_tuple** e andando a prendere con il valore tra [] 0,1,2 a seconda di quale valore voglio andare a pescare

  
  

  
  

- Dovevamo restituire una lista di tuple
    
- Passare da un alista con dentro delle tuple ad una lista con dentro delle stringhe, non delle tuple
    
- COME CONVERTIRE UNA LISTA DI TUPLE IN UNA LISTA DI STRINGHE
    

![](file:///tmp/lu1231978b51.tmp/lu1231978b6c_tmp_b52650e5be3f723c.png)

Stringa = tupla[0]

Mi restituisce la posizione della stringa all’interno della tupla

![](file:///tmp/lu1231978b51.tmp/lu1231978b6c_tmp_b1b68a93cfdcca42.png)

Abbiamo creato una lista vuota con un ciclo FOR LOOP e andiamo ad analizzare tutte le tuple elemento per lemento nella lista, perciò il valore di x ho preso la stringa, la parte tra la virgolette, che è la prima parte della tupla. Leggo la stringa che è dentro la tupla, per poterla prendere dalla lista uso x[0]

Proviamo a impostare un metodo più semplice per poi passare ad uno più complesso dal pdv logico.

Lista_vuota= []

**For** ([https://www.w3schools.com/python/python_for_loops.asp](https://www.w3schools.com/python/python_for_loops.asp))

_Iterare = passare da un elemento all’altro_

  
  

For x in lista_tuple:

lista_vuota.append(x)

print(“Lista vuota:”,lista_vuota)

lista_vuota.

  
  

**Append** [https://mimo.org/glossary/python/append()](https://mimo.org/glossary/python/append\(\))

  
  

12/09:

INTERAZIONE COI COMANDI DI VISUAL STUDIO CODE

COME ANNULLARE DELLE MODIFICHE SU UN FILE CHE NON MI SERVE.

Vediamo come muoverci attraverso la terza sezione SOURCE CONTROL. Nelle finestre mi appaiono le modifiche in verde

BRANCH: etichetta/(puntatore ad un) posta sopra un commit, di default viene MASTER che è allo stato locale. ORIGIN/MASTER è quello caricato sul cloud.

![](file:///tmp/lu1231978b51.tmp/lu1231978b6c_tmp_8e4ce83b627e042d.png) [https://www.atlassian.com/git/tutorials/using-branches#:~:text=In%20Git%2C%20branches%20are%20a,branch%20to%20encapsulate%20your%20changes](https://www.atlassian.com/git/tutorials/using-branches#:~:text=In%20Git%2C%20branches%20are%20a,branch%20to%20encapsulate%20your%20changes)

  
  

Ci possono essere più puntatori e più commit.

Quando sono su una branch vedo tutte le modifiche fatte a quel commit.

  
  

Ad esempio stiamo lavorando per rilasciare un’app e vogliamo rilasciare una nuova feature. Se quest’ultima non è completa non posso metterla su Main sennò spacca il lavoro di tutti, perciò stacco una branch, aggiungo una nuova etichetta Little Feature.

  
  

REPOSITORY: ORIGIN/MASTER

Il nome del branch quando vado a creare è la prima cosa che mi chiede.

  
  

In locale posso fare quello che voglio e creare modifiche perché sono da me.

_Brave browser non c’è pubblicità_

_15/09/2025 (DA SISTEMARE)_

_Definizione di funzione: con_ _**def**__, questo è il nome e quali sono gli argomenti tra parentesi_

_Chiamata di funzione: quando richiamo direttamente la funzione e poi la lancio e ci dà un risultato_

_Salvo i risultati nella variabile per interagire con database._

_Import sqlite3 è l’import di un modulo che è un insieme di parametri e funzioni. I moduli devono avere una definizione._

_Chiamo una funzione, la rinominiamo con una variabile RETURN perché la funzione restituisca qualcosa._

  
  

_Dopo l’IF, scriviamo delle condizioni boleane_

_In ogni linguaggio di programmazione c’è il concetto del MAIN, che ci aspettiamo che funzioni._