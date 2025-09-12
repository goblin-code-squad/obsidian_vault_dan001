--1) Creare la tabella con i dati del dataset delle preferenze alimentari

--2) Quante righe ci sono del dataset

  

SELECT COUNT (*)

FROM preferenze_alimentari_italia pai

  

--3) Quante righe non duplicate ci sono nel dataset

  

SELECT COUNT (*)

FROM (SELECT DISTINCT *

FROM preferenze_alimentari_italia);

  

--4) Selezionare le righe con ID 209. Quante righe ottengo? 3

  

SELECT COUNT (id) FROM preferenze_alimentari_italia pai where ID=209

  

--5) Nelle righe con ID 209 verificare se le variabili presentano tutte gli stessi valori

  

select distinct *

from preferenze_alimentari_italia pai where id=209

  

--6) Selezionare solo le righe con ID che è un multiplo di 10 (trova come farlo)

  

SELECT id from preferenze_alimentari_italia pai

WHERE MOD(id, 10)=0 --scrivere come si usa mod

  

--7) Selezionare id, data di nascita, anno, mese e giorno della data di nascita.

  

  

SELECT id, data_nascita,

SUBSTRING(data_nascita, 7, 4) as anno,

SUBSTRING(data_nascita, 4, 2) as mese,

SUBSTRING(data_nascita, 1, 2) as giorno

FROM preferenze_alimentari_italia;

  

  

  

  

  

--8) Selezionare le righe delle persone che sono nate dopo di voi

  

select data_nascita from preferenze_alimentari_italia pai where data_nascita > 23/11/1985 -- usare substring

  

--9) Selezionare solo le righe di chi è nato il primo gennaio.

  

SELECT * from preferenze_alimentari_italia

WHERE data_nascita LIKE '01/01%'%

  

--10) Selezionare id, data di nascita ed età.

  

SELECT ID, pai.data_nascita, pai.eta

FROM preferenze_alimentari_italia pai

  

  

--11) Contare quante persone nate il primo gennaio hanno più di 100 anni.

  

SELECT COUNT * from preferenze_alimentari_italia pai where

  

--12) Selezionare le preferenze alimentari delle persone che sono nate nel vostro stesso

--mese.

  

SELECT

id,

cucina_italiana,

cucina_cinese,

cucina_giapponese,

cucina_indiana,

cucina_messicana,

cucina_mediorientale,

cucina_africana,

cucina_vegetariana,

cucina_vegana,

cucina_fastfood

FROM preferenze_alimentari_italia

WHERE SUBSTR(data_nascita, 4, 2)='11' --e' un text

;

  

--13) Selezionare per ogni data di nascita i segni zodiacali

  

SELECT id,data_nascita,

CASE

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0321' AND '0420'THEN 'Ariete'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0421' AND '0520'THEN 'Toro'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0521' AND '0620'THEN 'Gemelli'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0621' AND '0722'THEN 'Cancro'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0723' AND '0823'THEN 'Leone'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0824' AND '0922'THEN 'Vergine'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0923' AND '1022'THEN 'Bilancia'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '1023' AND '1121'THEN 'Scorpione'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '1122' AND '1221'THEN 'Sagittario'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '1222' AND '0120'THEN 'Capricorno'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0121' AND '0219'THEN 'Acquario'

WHEN SUBSTRING(data_nascita,4,2)||SUBSTRING(data_nascita,1,2)BETWEEN '0220' AND '0320'THEN 'Pesci'

END AS segno_zodiacale

FROM preferenze_alimentari_italia

END

  

--14) Contare persone hanno meno di 18 anni.

SELECT * FROM preferenze_alimentari_italia pai

WHERE eta<18

--15) Per ogni id selezionate data di nascita e le seguenti classi di età (<20; 20 <= età < 30;

--30 <= età < 40, 40 <= età < 50, [continuate la sequenza], età >= 80). Non considerate le

--persone che hanno più di 100 anni

SELECT ID, data_nascita,

CASE

WHEN eta < 20 THEN '<20'

WHEN eta >= 20 AND eta < 30 THEN '20-29'

WHEN eta >= 30 AND eta < 40 THEN '30-39'

WHEN eta >= 40 AND eta < 50 THEN '40-49'

WHEN eta >= 50 AND eta < 60 THEN '50-59'

WHEN eta >= 60 AND eta < 70 THEN '60-69'

WHEN eta >= 70 AND eta < 80 THEN '70-79'

WHEN eta >= 80 THEN '80+'

END AS classe_eta

from preferenze_alimentari_italia pai

WHERE

eta <=100;

--16) Selezionare id e genere. Unite le risposte “Altro” e “Preferisco non specificare”

--17) Selezionate id, genere e una colonna che contenga il primo carattere del genere

--(esempio: Femmina -> F). La nuova colonna deve essere sempre in uppercase.

--Escludete dalla selezione le opzioni “Altro” e “Preferisco non rispondere”

--18) Selezionare le associazioni distinte Città di residenza e Regione di residenza

SELECT DISTINCT (JOIN citta_residenza, regin) FROM preferenze_alimentari_italia pai where

--19) Selezionare le città di residenza distinte che terminano con il carattere “o”

SELECT

--20) Selezionare le prime 5 righe che hanno “Città di residenza” Emilia-Romagna sostituendo

--il “-” con lo spazio

SELECT *

FROM preferenze_alimentari_italia pai

WHERE citta_residenza = 'Emilia-Romagna'

LIMIT 5;

--21) Verificare se ci sono righe di persone che hanno un titolo di studio laurea o laurea

--magistrale e hanno meno di 18 anni

WITH temporaryTable (averageValue) AS (

SELECT AVG (Attr1)

FROM Table

)

SELECT Attr1

FROM Table, temporaryTable

WHERE Table.Attr1 > temporaryTable.averageValue;

-- nuova colonna temporanea

ALTER TABLE preferenze_alimentari_italia ADD COLUMN data_nascita_temporanea TEXT;

-- crea dati nuova colonna

SELECT id,

anno ||'-'||mese||'-'||giorno

FROM (

SELECT id,

SUBSTRING(data_nascita, 7, 4) as anno,

SUBSTRING(data_nascita, 4, 2) as mese,

SUBSTRING(data_nascita, 1, 2) as giorno

FROM preferenze_alimentari_italia

) AS data_nascita_temp;

  

UPDATE preferenze_alimentari_italia SET data_nascita = data_nascita_temp WHERE data_nascita IS NOT NULL;

  

-- elimino la vecchia colonna

ALTER TABLE preferenze_alimentari_italia DROP COLUMN data_nascita;

ALTER TABLE preferenze_alimentari_italia RENAME COLUMN data_nascita_temp TO data_nascita;

  

WITH data_nascita_temp ()

  

WITH data_nascita_temp AS (

SELECT id,

SUBSTRING(data_nascita, 7, 4) as anno,

SUBSTRING(data_nascita, 4, 2) as mese,

SUBSTRING(data_nascita, 1, 2) as giorno

FROM preferenze_alimentari_italia

)

UPDATE preferenze_alimentari_italia pai

SET data_nascita = (

SELECT

id,

anno ||'-'||mese||'-'||giorno as data_giusta

FROM data_nascita_temp)

WHERE data_nascita is not null

  

UPDATE preferenze_alimentari_italia SET data_nascita = data_nascita_temp WHERE data_nascita IS NOT NULL;

  

-- Elimina la vecchia colonna

ALTER TABLE preferenze_alimentari_italia DROP COLUMN data_nascita;

ALTER TABLE preferenze_alimentari_italia RENAME COLUMN data_nascita_temp TO data_nascita;

  

-- per vedere se qualcuno ha meno di 18 anni

  

--22) Per ogni cucina contare quante persone non hanno espresso la preferenza. L’output

--dovrebbe risultare:

--CucinaN.di non risposte

--Italiana n1

--Cinese n2

--Giapponese n3

  

--23) Quante sono le persone che preferiscono la cucina vegana a quella fast food

  

select cucina_vegana, cucina_fastfood

from preferenze_alimentari_italia pai where cucina_vegana>=4 AND cucina_fastfood

  

--24) Quante persone hanno espresso una preferenza 5 per più di una cucina

--25) Quante persone abitano a Bologna, hanno più di 50 anni e hanno una preferenza

--maggiore di 3 per la cucina vegetariana

--26) Seleziona quante sono, l’eta minima, l’età massima e l’età media delle persone che

--hanno una preferenza pari a 5 per la cucina fast food

--27) Seleziona per ogni persona la/e cucina/e preferita/e

--28) Per ogni persona calcola il punteggio minimo, massimo e medio tra tutte le preferenze

--29) Ripeti il task 18 e conta quante righe ottieni per ogni valore M e F

--30) Per ogni titolo di studio calcola età minima e massima

--31) Per chi abita a Bologna calcola quante persone hanno espresso le diverse preferenze