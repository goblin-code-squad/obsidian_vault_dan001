artisti che vendono di più (limite 10)
- fatturato all’ anno
- quali sono i generI piu ascoltati per paese
- Quali sono i formati audio + venduti?
- Quali sono i formati audio - venduti?
- Media delle vendite per venditore in un particolare anno
- - rinomina il titolo;
- impostalo con font 16, in grassetto;
- cambia il font delle etichette dell'asse X e Y a 12
	- artisti che vendono di più (limite 10)
- fatturato all’ anno
- quali sono i generI piu ascoltati per paese


1) una scheda (oggetto grafico) con il fatturato totale non filtrabile
```dax
totale_non_filtrabile = CALCULATE(SUM('chinook_dwh fact_sales'[sales_value]),ALL('chinook_dwh dim_customer_country'))
```
2) una scheda (oggetto grafico) con il fatturato totale delle vendite, filtrabile per paese  
3) una scheda (oggetto grafico) con il fatturato % per paese (edited)
	