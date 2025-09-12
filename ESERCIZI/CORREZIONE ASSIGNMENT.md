[[PARTITION BY]]

come mettere id? [[ROW_NUMBER]]


-- trovati id null
SELECT *
FROM preferenze_alimentari_italia pai 
WHERE id is null


CREATE TABLE lt_preferenze_alimentari_italia AS
SELECT ROWID as ids, *
FROM preferenze_alimentari_italia


-- mi creo lo scheletro della tabella e dopo faccio le insert
CREATE TABLE tabella_scarti AS
SELECT *
FROM preferenze_alimentari_italia pai 
WHERE 0


INSERT INTO tabella_scarti
SELECT * from preferenze_alimentari_italia where id is null;

-- oppure
DROP IF EXISTS tabella_scarti;
CREATE TABLE tabella_scarti AS
SELECT *
FROM preferenze_alimentari_italia pai 
WHERE id is null


CREATE TABLE tt_id_duplicati AS
SELECT id
FROM preferenze_alimentari_italia
GROUP BY id
HAVING COUNT(*)>1

SELECT *
FROM lt_preferenze_alimentari_italia lpai 
WHERE id in (SELECT * FROM tt_id_duplicati)
ORDER BY ids DESC

DROP TABLE IF EXISTS tt_ids_righe_duplicate_da_mantenere;
CREATE TABLE tt_ids_righe_duplicate_da_mantenere AS
SELECT MAX(ids) as ids, id
FROM lt_preferenze_alimentari_italia lpai 
WHERE id in (SELECT * FROM tt_id_duplicati)
GROUP BY id;

SELECT * FROM tt_ids_righe_duplicate_da_mantenere

SELECT *
FROM lt_preferenze_alimentari_italia lpai 
WHERE 
	id in (SELECT * FROM tt_id_duplicati) 
	AND ids not in (SELECT ids FROM tt_ids_righe_duplicate_da_mantenere)
ORDER BY ids DESC



SELECT * FROM (
SELECT ROWID, ROW_NUMBER() OVER (PARTITION BY id ORDER BY ROWID DESC) as row_number, *
FROM preferenze_alimentari_italia
) p
WHERE p.row_number!=1


DROP TABLE IF EXISTS et_preferenze_alimentari_italia;
CREATE TABLE et_preferenze_alimentari_italia AS
SELECT *
FROM lt_preferenze_alimentari_italia pai 
WHERE id is null
	OR eta is null or eta >120 or eta <10
	OR citta_residenza is null or TRIM(citta_residenza) =""
	OR 
	( 
		-- id righe duplicate ma con MAX(ROWID)
		ids not in (
		SELECT MAX(ids) as ids
		FROM lt_preferenze_alimentari_italia lpai 
		WHERE id in (
				SELECT id
				FROM preferenze_alimentari_italia
				WHERE eta is not null AND eta <120 or eta >10
			AND citta_residenza is  not null and TRIM(citta_residenza) !=""
		
				GROUP BY id
				HAVING COUNT(*)>1)
		GROUP BY id
		)
		AND
		-- id righe duplicate
		id in (
				SELECT id
				FROM lt_preferenze_alimentari_italia
				WHERE eta is not null AND eta <120 or eta >10
			AND citta_residenza is  not null and TRIM(citta_residenza) !=""
				GROUP BY id
				HAVING COUNT(*)>1)
	)

SELECT * from tabella_scarti_group_by

DROP TABLE  IF EXISTS et_preferenze_alimentari_italia;
CREATE TABLE et_preferenze_alimentari_italia AS
SELECT *
FROM lt_preferenze_alimentari_italia pai 
WHERE id is null
	OR eta is null or eta >120 or eta <10
	OR citta_residenza is null or TRIM(citta_residenza) =""
	OR 
	ids in(
		SELECT ids FROM (
		SELECT ROW_NUMBER() OVER (PARTITION BY id ORDER BY ROWID DESC) as row_number, *
		FROM lt_preferenze_alimentari_italia
		WHERE eta is not null AND eta <120 or eta >10
			AND citta_residenza is  not null and TRIM(citta_residenza) !=""
		) p
		WHERE p.row_number!=1
	)
	
SELECT * FROM et_preferenze_alimentari_italia

SELECT 'lt_preferenze_alimentari_italia',COUNT(*) as count FROM lt_preferenze_alimentari_italia
UNION ALL
SELECT 'et_preferenze_alimentari_italia',COUNT(*) as count FROM et_preferenze_alimentari_italia
-- 307 e 11

DROP TABLE tt_preferenze_alimentari_italia_V01;
CREATE TABLE tt_preferenze_alimentari_italia_V01 AS
SELECT lt.* 
FROM lt_preferenze_alimentari_italia lt
LEFT JOIN et_preferenze_alimentari_italia et
	ON lt.ids=et.ids
WHERE et.ids is null;

SELECT COUNT(*), 307-11 as 'dovrebbe_venire'
FROM tt_preferenze_alimentari_italia_V01;

SELECT * FROM tt_preferenze_alimentari_italia_V01;

SELECT DISTINCT genere 
FROM tt_preferenze_alimentari_italia_V01;

-- lk sta per LOOKUP/ANAGRAFICA
CREATE TABLE lk_genere AS
SELECT ROW_NUMBER() OVER() as ids, * FROM (
	SELECT DISTINCT genere 
	FROM tt_preferenze_alimentari_italia_V01
	) g;

SELECT * FROM tt_preferenze_alimentari_italia_V01;

CREATE TABLE tt_preferenze_alimentari_italia_V02 AS
SELECT
	tt.ids,
	id,
	data_nascita,
	eta,
	lk.ids as genere,
	citta_residenza,
	regione_residenza,
	titolo_studio,
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
FROM
	tt_preferenze_alimentari_italia_V01 tt
	JOIN lk_genere lk 
		ON tt.genere =lk.genere;

SELECT * FROM tt_preferenze_alimentari_italia_V02;

SELECT * FROM lk_genere

SELECT DISTINCT citta_residenza, regione_residenza
FROM tt_preferenze_alimentari_italia_V02;

SELECT DISTINCT citta_residenza, regione_residenza, COUNT(*)
FROM tt_preferenze_alimentari_italia_V02
GROUP BY citta_residenza, regione_residenza;


CREATE TABLE lk_citta_regione AS
SELECT ROW_NUMBER() OVER ( ORDER BY citta_residenza ,regione_residenza) as ids,citta_residenza,regione_residenza  FROM(
SELECT c.*, 
	ROW_NUMBER() OVER (PARTITION BY citta_residenza ORDER BY count DESC) as r
FROM (
	SELECT DISTINCT citta_residenza, regione_residenza, COUNT(*) as count
	FROM tt_preferenze_alimentari_italia_V02
	GROUP BY citta_residenza, regione_residenza
) c
)cc
WHERE cc.r=1

SELECT * FROM lk_citta_regione

CREATE TABLE tt_preferenze_alimentari_italia_V03 AS
SELECT tt.ids, id, data_nascita, eta, genere, lk.ids as citta_regione, titolo_studio, cucina_italiana, cucina_cinese, cucina_giapponese, cucina_indiana, cucina_messicana, cucina_mediorientale, cucina_africana, cucina_vegetariana, cucina_vegana, cucina_fastfood
FROM tt_preferenze_alimentari_italia_V02 tt
JOIN lk_citta_regione lk ON tt.citta_residenza =lk.citta_residenza;

SELECT * FROM tt_preferenze_alimentari_italia_V03;

CREATE TABLE tt_preferenze_alimentari_italia_V04 AS
SELECT *,
	--CASE WHEN eta >= 0 AND eta < 21 THEN “<=20”
	CASE WHEN eta BETWEEN 0 AND 20 THEN "<=20"	
	WHEN eta BETWEEN 20 AND 30 THEN "21-30"
	WHEN eta BETWEEN 30 AND 40 THEN "31-40"
	WHEN eta BETWEEN 40 AND 50 THEN "41-50"
	WHEN eta BETWEEN 50 AND 60 THEN "51-60"
	WHEN eta BETWEEN 60 AND 70 THEN "61-70"
	WHEN eta BETWEEN 70 AND 80 THEN "71-80"
	WHEN eta > 80 THEN ">80"
	ELSE "rotto" END
	AS classe_eta
FROM tt_preferenze_alimentari_italia_V03;


SELECT * FROM tt_preferenze_alimentari_italia_V04


CREATE TABLE lk_cucine_parziale AS
SELECT ROW_NUMBER() OVER() as ids, * FROM
(
	SELECT ids as ids_og, 'italiana' as tipo_cucina, cucina_italiana as  valutazione 
	FROM tt_preferenze_alimentari_italia_V04 
	UNION ALL
	SELECT ids as ids_og, 'cinese' as tipo_cucina, cucina_cinese as  valutazione 
	FROM tt_preferenze_alimentari_italia_V04 
	UNION ALL
	SELECT ids as ids_og, 'giapponese' as tipo_cucina, cucina_giapponese as  valutazione 
	FROM tt_preferenze_alimentari_italia_V04 
) a
ORDER By ids_og

SELECT * from lk_cucine_parziale

CREATE TABLE tt_valutazione_max_cucine AS
SELECT * FROM(
SELECT ROW_NUMBER( ) OVER(PARTITION BY ids_og ORDER BY COALESCE(valutazione,0) DESC,tipo_cucina) as r, *
FROM lk_cucine_parziale
) a
WHERE a.r=1

SELECT * FROM tt_valutazione_max_cucine

SELECT COUNT(*) FROM tt_valutazione_max_cucine


SELECT val.* FROM tt_preferenze_alimentari_italia_V04 tt
	JOIN tt_valutazione_max_cucine val
		on tt.ids=val.ids_og
	ORDER BY ids_og

soluzione_assignment_week5.sql

External

Displaying soluzione_assignment_week5.sql.