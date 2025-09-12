``sql * ``
serve per selezionaree a tutto (per esempio una colonna)

*SQL requires single quotes around text values (most database systems will also allow double quotes).*
*However, numeric fields should not be enclosed in quotes:*

Query= lanciare le cosine
si possono lanciare comandi inseme con risulati divers, selezionando iconcina

``sql INSERT``
serve per inserire

```sql 
--serve per cancellare un dato specifico
DELETE FROM persona WHERE (cognome) is null

--
select * from persone WHERE nome!=Marco
-- serve per 

UPDATE persone SET cognome ="Rubiero"

--ricordati che i dati sono case senstivie mentre i comandi no

UPDATE persone
SET cognome="Rossi"
WHERE nome="gigi"
-- setto la colonna cognome dove c'e' il nome gigi
UPDATE persone
SET cognome="Rossi"
WHERE LOWER(nome)="gigi"
-- setto il cognome specificando di prendere la casella anche se e' minuscola



