[[JOIN]]


ESMPIO JOIN GIUSTA con una sola  var nella select
(non serve group by)
```sql
select

sum(sales_value) as totale_vendite_italia

  

from fact_sales

  

join

dim_customer_customer ON fact_sales.customer_ids = dim_customer_customer.customer_ids

  

join

  

dim_customer_country on dim_customer_customer.country_ids = dim_customer_country.country_ids

  

where dim_customer_country.customer_country = 'Italy'
```



--non va
select *, 'non_esisto_ancora' as non_esisto_ancora
from chinook_landing.lt_media_type lt
where non_esisto_ancora='non_esisto_ancora'

--va
select * from (
select *, 'non_esisto_ancora' as non_esisto_ancora
from chinook_landing.lt_media_type lt
) a
where non_esisto_ancora='non_esisto_ancora'



--dammi i valori della colonna che hanno dei duplicati
```sql
select colonna_che_forse_ha_duplicati, 
	COUNT(colonna_che_forse_ha_duplicati)
	FROM tabella_con_colonna_con_forse_i_duplicati
	group by colonna_che_forse_ha_duplicati
	having COUNT(colonna_che_forse_ha_duplicati)>1
```

es:

- Per controllare se una colonna non ha doppioni:

Select colonna1 from tabella2  
group by colonna1  
having count(colonna1) > 1

es: 

```sql

select
	ids_giorno,
	count(*) as conteggio_duplicati
from
openbo_dwh.dim_tempo_inizio dti
group by
	ids_giorno -- raggruppa tutte le righe con la stessa data
having
	count(*) > 1;
```

select  colonna_che_forse_ha_duplicati, 
	COUNT(colonna_che_forse_ha_duplicati)
	FROM tabella_con_colonna_con_forse_i_duplicati
	group by colonna_che_forse_ha_duplicati
	order by 
	COUNT(colonna_che_forse_ha_duplicati) asc
	
Collapse

**SELECT** _u_."OBJECTID",  
**COUNT**(_u_."OBJECTID")  
**FROM** us_colleges_and_universities _u_  
**GROUP** **BY** _u_."OBJECTID"  
**ORDER** **BY** **COUNT**(_u_."OBJECTID") **ASC**;



  
create table dataset_lercio (id integer, name varchar(20), surname varchar(20), age integer)

insert into dataset_lercio (id,name,surname,age) values(1,'Marco', 'rubiero',33);

insert into dataset_lercio (id,name,surname,age) values(2,'Giovannino', 'ciuffolo',10);

insert into dataset_lercio (id,name,surname,age) values(-1,'Rotto', 'Rottissimo',-200);

select * from dataset_lercio

create table id_scarti as 
select id from dataset_lercio where age<0 or age>120

select * from id_scarti

create table dataset_meno_lercio as
	select * from dataset_lercio where age>0 and age<120

create table dataset_meno_lercio_v2 as
	select dl.* from dataset_lercio dl
		join id_scarti scarti 
			on dl.id!=scarti.id

create table dataset_meno_lercio_v3 as
	select dl.* from dataset_lercio dl
		where dl.id not in (select id from id_scarti)

create table dataset_meno_lercio_v4 as
	select dl.* from dataset_lercio dl
		left join id_scarti scarti 
			on dl.id=scarti.id
			where scarti.id is null










classica left join

![[Pasted image 20250718172342.png]]
