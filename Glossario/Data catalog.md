### **DATA CATALOG**  

Termine / cosa vuol dire la colonna / tipo di variabile / Dominio 

#### **Definizione**  
Un **Data Catalog** è un inventario organizzato di dati aziendali che funge da "biblioteca" per trovare, comprendere e governare i dati. Include metadati, descrizioni, relazioni e informazioni sull'utilizzo.  

---

### **Dettagli**  
#### **1. Componenti Chiave**  
- **Metadati**:  
  - Descrizioni di tabelle, colonne, metriche (es: "Questa colonna contiene il prezzo in EUR").  
  - Proprietà tecniche (tipo di dato, formato, owner).  
- **Lineage**: Tracciamento dell'origine e delle trasformazioni dei dati (es: "Questo report usa dati estratti dal CRM il 01/01/2023").  
- **Classificazione**: Tag (es: "PII" per dati personali, "Finance" per dati finanziari).  
- **Ricerca**: Motore per trovare dataset con parole chiave (es: "vendite 2023").  

#### **2. Vantaggi**  
- **Scoperta dati**: Riduce il tempo per trovare informazioni.  
- **Governance**: Aiuta a rispettare normative (GDPR, SOX).  
- **Collaborazione**: Annotazioni condivise (es: "Questo campo è obsoleto, usare `customer_id`").  

---

### **Esempi Pratici**  
#### **Strumenti Popolari**  
- **Enterprise**: Informatica Axon, Collibra, Alation.  
- **Open-source**: Amundsen (LinkedIn), DataHub (LinkedIn).  
- **Cloud**: AWS Glue Data Catalog, Google Data Catalog.  

#### **Esempio di Metadati in un Catalog**  
```python  
# Dataset fittizio nel catalog  
{  
  "name": "sales_data",  
  "description": "Vendite mensili per regione (2020-2023)",  
  "columns": [  
    {"name": "date", "type": "date", "description": "Data transazione (YYYY-MM-DD)"},  
    {"name": "region", "type": "string", "tags": ["geography", "PII"]}  
  ],  
  "owner": "team-analytics@azienda.com",  
  "last_updated": "2023-05-20"  
}  
```  

---

### **Contesti d’Uso**  
- **Onboarding nuovi dipendenti**: Capire rapidamente dove trovare i dati.  
- **Migrazioni**: Mappare dataset tra sistemi legacy e nuovi.  
- **Data Quality**: Identificare dataset obsoleti o duplicati.  

---

### **Domande Tipiche**  
1. **"Come convincere un'azienda a investire in un Data Catalog?"**  
   *Risposta*:  
   - Riduce il 30% del tempo speso a cercare dati (stime Forrester).  
   - Mitiga rischi legali (es: tracciamento dati sensibili).  

2. **"Qual è la differenza con un Data Dictionary?"**  
   *Risposta*:  
   - Il **Data Dictionary** descrive solo struttura e campo.  
   - Il **Catalog** aggiunge ricerca, lineage e collaborazione.  

---

### **Best Practice**  
1. **Automatizzare l'harvesting**: Integrare con database, ETL e BI tool.  
2. **Coinvolgere gli utenti**: Incentivare team ad annotare i dataset.  
3. **Pulizia periodica**: Archiviare dataset inutilizzati.  

**Esempio di Policy**:  
> "Ogni nuovo dataset deve essere registrato nel Catalog entro 7 giorni dalla creazione."  

---

### **Esempio Reale**  
**Problema**: Un analista cerca "clienti inattivi" ma non sa dove trovarli.  
**Soluzione**:  
1. Cerca nel Catalog: `tag:"customer" + "inactive"`.  
2. Trova il dataset `customer_status` con descrizione: "Flag clienti inattivi (nessun ordine da 6 mesi)".  
3. Consulta il lineage per verificare che i dati vengano aggiornati giornalmente.  

---

Vuoi vedere come configurare un **Data Catalog open-source** (es: Amundsen) o un caso di tagging avanzato? 