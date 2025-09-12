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