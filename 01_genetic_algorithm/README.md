# **Úloha 1: Genetický algoritmus - binární problém**

> Kompletní interaktivní kód s možností spuštění [jupyter notebooku zde](./genetic_algorithm.ipynb).

## **Výsledky a statistiky**

###  **One-Max**

| Dimenze | Počet evaluací | Nejlepší výsledek | Nejhorší výsledek | Průměr | Medián | Směrodatná odchylka | Úspěšnost nalezení optima |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **10D** | 1000 | 10.00 | 10.00 | 10.00 | 10.00 | 0.00 | 100.0% |
| **30D** | 3000 | 30.00 | 30.00 | 30.00 | 30.00 | 0.00 | 100.0% |
| **100D** | 10000 | 100.00 | 100.00 | 100.00 | 100.00 | 0.00 | 100.0% |

###  **Leading Ones**

| Dimenze | Počet evaluací | Nejlepší výsledek | Nejhorší výsledek | Průměr | Medián | Směrodatná odchylka | Úspěšnost nalezení optima |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **10D** | 1000 | 10.00 | 10.00 | 10.00 | 10.00 | 0.00 | 100.0% |
| **30D** | 3000 | 30.00 | 30.00 | 30.00 | 30.00 | 0.00 | 100.0% |
| **100D** | 10000 | 100.00 | 72.00 | 89.60 | 89.50 | 7.89 | 20.0% |

## **Konvergenční grafy**
![One-Max konvergence](./assets/onemax_convergence.png)
![Leading Ones konvergence](./assets/leading_ones_convergence.png)

## **Závěr a shrnutí úkolu**

#### **Srovnání úloh: One-Max vs. Leading Ones**

##### **One-Max**
* Každý bit přispívá k celkové hodnotě fitness nezávisle. Algoritmus těží ze stabilního gradientu, kdy jakákoli náhodně nalezená jednička okamžitě zvyšuje fitness.
* Díky tomu jsem také dosáhl 100% úspěšnosti nalezení globálního optima ve všech zadaných dimenzích (10D, 30D i 100D)

##### **Leading Ones**
* Hodnotu fitness určuje nepřerušená řada jedniček z levé strany. Bity za první nulou nepředstavují žádnou odměnu.
* Zde byla optimalizace o dost náročnější, v dimenzi 100D jsem i přes různé nastavení hyperparametrů nedospěl k výsledku, kdy bych našel optimum ve více než 2 z 10 proběhlých nezávislých běhů.

#### **Vliv hyperparametrů**

##### **Velikost populace**
* Tento hyperparametr mě nějvíce zaskočil především při nastavení u dimenze 100D u Leading Ones problému. Zatímco u One-Max úlohy jsem s rostoucí dimenzí velikost populace zvětšoval, nejlepšího výsledku u dimenze 100D u Leading Ones jsem naopak dosáhl po zmenšení velikosti populace v daném experimentu.

##### **Elitismus**
* U One-Max optimalizace mi stačilo pro dosažení optima zachovat 10 % nejlepších jedinců z předchozí generaci. 
* U Leading-Ones optimalizace musela být hodnota elitismu větší (15 - 20 %), jelikož bylo v mém zájmu ponechat co nejvíce jedinců, kteří už měli vybudovaný dlouhý prefix jedniček.

##### **Míra mutace**
* Míru mutace jsem držel na hodnotě 1 % u One-Max problému, jelikož inverze bitu především z 0 na 1 byla velice žádoucí.
* U Leading Ones jsem hodnotu tohoto parametru snížil na 0,75 % u dimenzí 10D a 100D, což mi přineslo kvalitnější výsledky. Zde si naopak myslím, že ztráta hodnoty fitness funkce za inverzi bitu v již existujícím prefixu samých jedniček nepřevyšuje možnou odměnu za prodloužení tohoto prefixu, a tudíž je nastavení pravděpodobnosti mutace na menší procentuální hodnotu tou správnou variantou.

