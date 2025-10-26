
```ini
PGPASSWORD=refresh psql -U postgres postgres
```


entrare nella shell di postgres

sudo -u postgres /bin/bash

edit file 
indirizoz file
 sudo vim /etc/postgresql/16/main/pg_hba.conf 

per modifare tasto i (modalita edit)

per uscire esc
per uscire da vim e salvare
: e poi wq
per non salvare ma uscire lo stesso
: q!

per riavviare 
```
sudo systemctl restart postgresql
```

sudo systemctl restart postgresql

per dare accesso all'ambiente grafico a qualsiasi utente

sudo xhost +

ctrl A inizio
ctrl e fine
tasto in mezzo per incollare
