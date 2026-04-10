## 1. Il Mix Produttivo Ottimale (Product Mix)
È il problema "padre" della PL. L'obiettivo è decidere **quanto produrre** di diversi articoli per massimizzare il profitto, rispettando i limiti delle risorse (ore macchina, materie prime, manodopera).

* **Ragionamento:** Ogni prodotto "ruba" risorse agli altri. Il modello deve trovare il punto di equilibrio dove il valore aggiunto totale è massimo senza sforare i magazzini o i tempi di lavoro.
* **Metodo di risoluzione:** Algoritmo del Simplesso (o Simplesso Duale se cambiano le disponibilità).

### Modellizzazione
* **Dati:** Profitto unitario ($c_j$), consumo di risorsa $i$ per il prodotto $j$ ($a_{ij}$), disponibilità totale della risorsa $i$ ($b_i$).
* **Vincoli:** Somma dei consumi $\le$ Disponibilità ($\sum a_{ij} x_j \le b_i$).
* **Funzione Obiettivo:** $\max z = \sum c_j x_j$.

### Esempio Semplice
Una falegnameria produce Tavoli ($x_1$) e Sedie ($x_2$).
* **Dati:** Tavolo (Profitto 50€, usa 2mq legno), Sedia (Profitto 30€, usa 1mq legno). Disponibilità: 100mq legno.
* **Vincoli:** $2x_1 + 1x_2 \le 100$; $x_1, x_2 \ge 0$.
* **Obiettivo:** $\max z = 50x_1 + 30x_2$.

---

## 2. Il Problema della Dieta (Blending)
L'opposto del mix produttivo. Qui vogliamo **minimizzare i costi** garantendo però dei livelli minimi di "qualità" o nutrienti. Si applica a mangimi, leghe metalliche o benzine.

* **Ragionamento:** Devo comporre un mix usando ingredienti diversi. Ognuno costa e ognuno apporta nutrienti. Devo "riempire i secchi" dei requisiti minimi spendendo il meno possibile.
* **Metodo di risoluzione:** Simplesso (spesso richiede la Fase 1 o il metodo della Grande M perché i vincoli sono $\ge$).

### Modellizzazione
* **Dati:** Costo unitario ingrediente ($c_j$), contenuto nutriente $i$ nell'ingrediente $j$ ($a_{ij}$), requisito minimo nutriente $i$ ($b_i$).
* **Vincoli:** Apporto totale $\ge$ Requisito minimo ($\sum a_{ij} x_j \ge b_i$).
* **Funzione Obiettivo:** $\min z = \sum c_j x_j$.

### Esempio Semplice
Creare un mangime con Proteine e Grassi usando Mais ($x_1$) e Soia ($x_2$).
* **Dati:** Mais (Costo 0.2€/kg, 5% prot., 2% grassi), Soia (Costo 0.5€/kg, 20% prot., 1% grassi). Requisiti: almeno 10kg proteine e 2kg grassi.
* **Vincoli:** $0.05x_1 + 0.20x_2 \ge 10$; $0.02x_1 + 0.01x_2 \ge 2$.
* **Obiettivo:** $\min z = 0.2x_1 + 0.5x_2$.

---

## 3. Il Problema del Trasporto (Transportation)
Ottimizzare lo spostamento di merci da $N$ depositi a $M$ clienti.

* **Ragionamento:** Spostare roba costa. Devo decidere quanta merce mandare da ogni magazzino a ogni cliente per soddisfare tutti i clienti senza svuotare i magazzini oltre la loro capacità, cercando il percorso meno costoso.
* **Metodo di risoluzione:** Algoritmo del Trasporto (Vogel, Metodo dei Moduli) o Simplesso su rete.

### Modellizzazione
* **Dati:** Capacità magazzino $i$ ($S_i$), domanda cliente $j$ ($D_j$), costo trasporto unitario da $i$ a $j$ ($c_{ij}$).
* **Vincoli:**
    1.  Uscita da magazzino $i \le S_i$.
    2.  Entrata da cliente $j \ge D_j$.
* **Funzione Obiettivo:** $\min z = \sum \sum c_{ij} x_{ij}$.

### Esempio Semplice
2 Fabbriche (A, B) e 2 Negozi (1, 2).
* **Dati:** A produce 500 unità, B 500. Negozio 1 vuole 400, Negozio 2 vuole 600. Costi: A→1 (2€), A→2 (4€), B→1 (3€), B→2 (1€).
* **Obiettivo:** $\min z = 2x_{A1} + 4x_{A2} + 3x_{B1} + 1x_{B2}$.

---

## 4. Copertura e Turnazione (Set Covering)
Tipico degli orari del personale o della posizione di caserme/antenne.

* **Ragionamento:** Devo "coprire" delle necessità (es. tutte le ore del giorno o tutte le zone di una città) usando il minor numero di risorse o al minor costo.
* **Metodo di risoluzione:** PL Intera (perché non posso assumere 0.5 persone).

### Modellizzazione
* **Dati:** Costo del turno/risorsa $j$ ($c_j$), matrice di copertura ($a_{ij} = 1$ se il turno $j$ copre l'ora $i$, $0$ altrimenti).
* **Vincoli:** Ogni ora deve essere coperta da almeno una persona ($\sum a_{ij} x_j \ge 1$).
* **Funzione Obiettivo:** $\min z = \sum c_j x_j$.

### Esempio Semplice
Turni di sorveglianza. Turno Mattina ($x_1$) copre ore 8-16, Turno Pomeriggio ($x_2$) 16-24, Turno Notte ($x_3$) 0-8.
* **Obiettivo:** $\min z = x_1 + x_2 + x_3$ (minimizzare il numero di guardie).
* **Vincoli:** $x_1 \ge 1, x_2 \ge 1, x_3 \ge 1$ (assumendo che serva almeno una persona per slot).

---

## 5. Pianificazione Multi-periodo (Production Planning)
Decidere quanto produrre oggi e quanto tenere in magazzino per domani.

* **Ragionamento:** A volte produrre tanto costa meno (economie di scala), ma tenere la merce in magazzino ha un costo (affitto, deperimento). Devo bilanciare produzione e scorte su più mesi.
* **Metodo di risoluzione:** Simplesso applicato a variabili indicizzate nel tempo.

### Modellizzazione
* **Dati:** Domanda al mese $t$ ($d_t$), costo produzione ($p_t$), costo stoccaggio ($h_t$).
* **Vincoli:** Equazione di bilancio: $\text{Scorta}_{t-1} + \text{Produzione}_t - \text{Domanda}_t = \text{Scorta}_t$.
* **Funzione Obiettivo:** $\min z = \sum (p_t x_t + h_t s_t)$.

### Esempio Semplice
Domanda Gennaio: 100, Febbraio: 150.
* **Vincolo Gennaio:** $0 (\text{scorta iniz.}) + x_{Gen} - 100 = s_{Gen}$.
* **Vincolo Febbraio:** $s_{Gen} + x_{Feb} - 150 = s_{Feb}$.
* **Obiettivo:** $\min \text{Costi produzione} + \text{Costi magazzino}$.

---

### Tabella Riassuntiva dei Ragionamenti

| Categoria | Verbo Chiave | Ostacolo Principale | Obiettivo Tipico |
| :--- | :--- | :--- | :--- |
| **Product Mix** | Scegliere | Scarsità risorse | Max Profitto |
| **Dieta/Blending** | Miscelare | Requisiti qualità | Min Costo |
| **Trasporto** | Spostare | Costi logistici | Min Costo |
| **Set Covering** | Coprire | Necessità di presenza | Min Risorse |
| **Multi-periodo** | Anticipare | Costi di giacenza | Min Costo Totale |
