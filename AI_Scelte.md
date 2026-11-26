# Scelte Progettuali & Come abbiamo usato l'IA

Questo documento descrive come abbiamo usato l'intelligenza artificiale generativa nel progetto e le scelte architetturali prese.

## 1. Strumenti

- **Claude**: principalmente per il codice
- **DeepSeek**: principalmente per la documentazione

## 2. Scelte progettuali

| Scelta | Alternative considerate | Motivo |
| --- | --- | --- |
| **Fonte dei dati: Jolpica F1** | TheSportsDB | Il piano gratuito di TheSportsDB limita i risultati per le stagioni passate, e questo impediva di registrare eventi del passato. Jolpica restituisce circuiti e calendari storici, senza chiave. |
| **Copia dei circuiti e degli eventi nel nostro database** (identificati da stagione + round) | Salvare solo l'identificativo e chiedere l'evento all'API ogni volta | Filtri, classifiche e statistiche uniscono i voti degli utenti ai dati dell'evento: con la copia lo fa il database con una query. Ricordi, commenti e presenze hanno chiavi esterne verificate dal database e l'app funziona anche se l'API è irraggiungibile. |
| **Risultati e dettagli di gara letti dall'API, non copiati** | Copiare anche la classifica completa | Servono solo nella pagina del GP e non si uniscono ai voti. Copiarli aggiungerebbe un'entità e l'importazione di circa 20 righe per gara. |
| **Limiti dell'API** | Nessuna precauzione | Jolpica ha limiti di richieste (circa 4 al secondo e un tetto orario). Non sono un problema perché la chiamiamo una volta per stagione e salviamo i dati. |
| **Identità «chi sono io»** | Accesso anonimo di Supabase; login con e-mail e password | Basta a ciò che serve all'app (un ricordo ha un autore). L'app presume che la scelta sia sincera, quindi le policy RLS non possono impedire di modificare i ricordi altrui: lo dichiariamo. |
| **Valori derivati calcolati a runtime, non salvati** (voti medi, classifica, statistiche del profilo) | Salvarli nel database | Salvarli richiederebbe di aggiornarli a ogni creazione, modifica o eliminazione di un ricordo, con il rischio di valori incoerenti. |
| **Settori dei circuiti:** **[da completare: cosa avete scelto]** | Generici uguali per tutti; specifici per circuito; creati dagli utenti; misto | **[da completare]** |
| **Stack:** React 19 su Vite, Supabase, json-server in sviluppo, tutte le chiamate in `src/api.js`, front end su Vercel | Firebase | Previsto e consigliato dal corso. Json-server e Supabase differiscono per un solo file. **[da completare: perché Tailwind, perché React Router, dove vive lo stato]** |

## 3. Per quali compiti

| Compito | Come l'abbiamo usata | Cosa abbiamo verificato o deciso noi |
| --- | --- | --- |
| Progettazione | Ha discusso con noi il modello dei dati, la copia contro il riferimento, cosa salvare e cosa leggere dall'API, i settori dei circuiti. | Abbiamo deciso di salvare una copia dei circuiti e degli eventi e come rappresentare i settori dei circuiti |
| Scrivere la proposta e la documentazione del progetto | Ha riscritto la proposta di progetto nel formato richiesto e prodotto bozze del README e dei documenti di architettura. | Abbiamo revisionato e corretto il testo |
| Verifica degli endpoint | Script per testare le chiamate a tutti gli endpoint di Jolpica, per controllare che circuiti e stagioni passate fossero disponibili senza rate limits troppo limitanti. | Abbiamo testato alcuni endpoint con PostMan personalmente |
| Bozze Grafiche | In una fase iniziale per produrre delle bozze grafica dell'interfaccia in HTML da cui prendere ispirazione. | **[da completare]** |

## 4. Proposte dell'IA che abbiamo scartato o modificato

| Cosa ha proposto l'IA | Cosa abbiamo fatto | Perché |
| --- | --- | --- |
| Per i dati di una gara oltre quelli di base, tre livelli: leggerli dall'API, copiare solo qualche campo, copiare l'intera classifica. Consigliava di non copiare la classifica completa. | Abbiamo scelto di non copiare risultati, classifiche, giri e telemetria, ma di leggerli dall'API quando servono. | Questo perchè i dati relativi ai risultati non sono fondamentali per il funzionamento dell'app |
| Categorie di settore (prato, tribuna sul rettilineo, tribuna di curva, altro), per fare statistiche e filtri tra circuiti. | **[da completare]** | **[da completare]** |

## 5. Un caso in cui l'IA ha sbagliato

**[da completare con un caso del vostro codice o del vostro progetto, come ci avete scoperto e come l'avete corretto.]**

## 6. Come ci siamo regolati

- Usiamo l'IA, e lo dichiariamo in questo documento.
- Non teniamo nel progetto codice che nessuno di noi sa spiegare.
