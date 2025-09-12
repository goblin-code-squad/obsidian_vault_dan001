Ecco un esempio completo di **gerarchia prodotti** in formato ASCII per Obsidian, con tabelle e relazioni:

```markdown
# GERARCHIA PRODOTTI (Database Design)

## 1. Tabella Categorie (Livello 1)
| id | nome        | descrizione          |
|----|-------------|----------------------|
| 1  | Elettronica | Prodotti elettronici |
| 2  | Abbigliamento | Vestiti e accessori |
| 3  | Casa        | Articoli per la casa |

## 2. Tabella Sottocategorie (Livello 2)
| id | categoria_id | nome           |
|----|--------------|----------------|
| 1  | 1            | Smartphone     |
| 2  | 1            | Computer       |
| 3  | 2            | Uomo           |
| 4  | 2            | Donna          |
| 5  | 3            | Arredamento    |

## 3. Tabella Prodotti (Livello 3)
| id | sottocategoria_id | codice | nome              | prezzo |
|----|-------------------|--------|-------------------|--------|
| 1  | 1                 | SM-X1  | Galaxy S24        | 999.99 |
| 2  | 1                 | IPH-15 | iPhone 15 Pro     | 1099.99|
| 3  | 2                 | MBP-14 | MacBook Pro 14"   | 1999.99|
| 4  | 3                 | T-SH01 | T-Shirt Basic     | 24.99  |

## 4. Tabella Varianti (Livello 4 - Opzionale)
| id | prodotto_id | attributo   | valore   |
|----|-------------|-------------|----------|
| 1  | 1           | Colore      | Nero     |
| 2  | 1           | Memoria     | 256GB    |
| 3  | 4           | Taglia      | XL       |
| 4  | 4           | Colore      | Bianco   |

## Relazioni (Diagramma ASCII)
```
┌───────────┐     ┌─────────────────┐     ┌─────────────┐     ┌──────────────┐
│ Categorie │─────│ Sottocategorie  │─────│  Prodotti   │─────│   Varianti   │
└───────────┘     └─────────────────┘     └─────────────┘     └──────────────┘
     1:N                  1:N                     1:N
```

## Query di Esempio
```sql
-- Ottenere tutti i prodotti elettronici con le sottocategorie
SELECT p.nome, s.nome AS sottocategoria, c.nome AS categoria
FROM prodotti p
JOIN sottocategorie s ON p.sottocategoria_id = s.id
JOIN categorie c ON s.categoria_id = c.id
WHERE c.nome = 'Elettronica';

-- Varianti per un prodotto specifico
SELECT v.attributo, v.valore 
FROM varianti v
WHERE v.prodotto_id = 1;
```

## Note per l'Implementazione
1. **Chiavi primarie**: Tutte le tabelle hanno `id` come PK
2. **Chiavi esterne**: 
   - `sottocategorie.categoria_id` → `categorie.id`
   - `prodotti.sottocategoria_id` → `sottocategorie.id`
   - `varianti.prodotto_id` → `prodotti.id`
3. **Estensioni possibili**:
   - Aggiungere `livello_priorita` per l'ordinamento
   - Campo `attivo` BOOLEAN per filtrare prodotti disponibili

Per usarlo in Obsidian:
1. Copia tutto il blocco
2. Incolla in una nuova nota
3. Abilita il plugin "Advanced Tables" per una migliore formattazione
```