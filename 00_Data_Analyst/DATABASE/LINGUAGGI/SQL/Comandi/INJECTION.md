
La **SQL injection** è una tecnica di attacco informatico in cui un utente malintenzionato inserisce codice SQL dannoso nei campi di input di un’applicazione, sfruttando la mancanza di controlli per manipolare o accedere ai dati del database.

**Esempio:**  
Se un’applicazione costruisce una query SQL concatenando direttamente l’input dell’utente, un attaccante può inserire comandi come:

' OR 1=1; --

Questo può permettere di leggere, modificare o cancellare dati non autorizzati.

**Come evitarla:**  
Usa sempre i **parametri** nelle query (prepared statements) invece di concatenare stringhe.