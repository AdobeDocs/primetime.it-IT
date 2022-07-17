---
title: Esporta informazioni per account con punteggio di condivisione elevato
description: Esporta le informazioni per gli account con un punteggio di condivisione elevato.
source-git-commit: 17a44bde5cf320f519cc537d37df0fe823cf51a6
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 1%

---


# Esporta informazioni per account con punteggio di condivisione elevato {#export-account-info-high-score}

L&#39;account IQ ti offre la possibilità di esportare i dettagli di condivisione dell&#39;account per i 1000 account più abbonati in base ai loro [condivisione delle probabilità](/help/AccountIQ/product-concepts.md#account-sharing-probability-def). I dati nel file CSV esportato vengono ordinati in ordine decrescente delle probabilità di condivisione degli account degli abbonati, degli MVPD selezionati nella [segmento](/help/AccountIQ/product-concepts.md#segment-def), per [arco temporale specificato](/help/AccountIQ/product-concepts.md#time-frame-def).

L’opzione per esportare le informazioni di condivisione dell’account è disponibile in [Rapporti generali sull’utilizzo](/help/AccountIQ/general-usage-reports.md) e [Report account condivisi](/help/AccountIQ/shared-acc-reports.md) pagine.

>[!NOTE]
>
>I numeri nel file CSV scaricato sono diversi per le pagine dei rapporti Uso generale e Account condivisi . Questo perché la pagina Rapporti sull&#39;uso generale dispone di filtri aggiuntivi per i programmatori che selezionano Soglia per il numero di dispositivi, IP e codici postali. Pertanto, i dati esportati dai rapporti di utilizzo generale si basano sul filtro di soglia aggiuntivo applicato.

![Opzione Esporta in uso generale](assets/export.png)

Per esportare le informazioni di condivisione degli account degli abbonati:

1. Specifica un segmento dal selettore del segmento. Per selezionare un segmento:

   1. Selezionare gli MVPD desiderati da **MVPD nel segmento** opzione .

   1. Seleziona i canali desiderati da **Canali nel segmento** opzione .

   1. Seleziona un arco temporale da **Granularità e arco temporale** per visualizzare i rapporti relativi.

1. Seleziona la **Esporta i primi 1000 account** opzione per esportare le informazioni dell&#39;account per 1000 utenti con la probabilità di condivisione più elevata.

Quando si utilizza l&#39;opzione di esportazione, le statistiche per 1000 account con le maggiori probabilità di condivisione (per un intervallo di tempo definito) vengono scaricate nella cartella Download del computer locale.

>[!NOTE]
>
>Il file CSV scaricato può essere aperto utilizzando qualsiasi applicazione che legga il file CSV, ad esempio Microsoft Excel.

![dati esportati in formato csv](assets/exported-csv.png)

*Figura: Esportazione dei dati degli account condivisi in formato CSV*

## Colonne del rapporto esportato {#columns-in-export}

**Settimana/Mese**

La settimana o il mese selezionato nella **Granularità e arco temporale** nel selettore del segmento, per il quale vengono richieste le statistiche di condivisione.

**MVPD**

Se sei un utente programmatore, la colonna mostra a quale MVPD appartiene l&#39;account utente iscritto.

**ID sottoscrittore**

Conto specifico di cui stiamo parlando in una fila.

**Numero minimo di dispositivi**

Il numero effettivo di dispositivi (il contenuto in streaming) è quasi certamente maggiore del numero minimo di dispositivi, specificato per un determinato account.

>[!NOTE]
>
>Il numero effettivo di dispositivi (il contenuto in streaming) è sicuramente maggiore del numero minimo di dispositivi, specificato per un determinato account.

**Numero minimo di persone**

Il numero minimo assoluto di persone che utilizzavano tali dispositivi per lo streaming dei contenuti.

>[!NOTE]
>
>Il numero effettivo di persone (il contenuto in streaming) è quasi certamente molto maggiore del numero minimo di persone, specificato per un determinato conto.

**N. IP**

Numero di indirizzi IP da cui viene eseguito lo streaming del contenuto.

**N. posizioni**

Numero di posizioni (basate sul codice postale) da cui viene eseguito lo streaming del contenuto.

**N. città**

Numero di città in cui è stato effettuato lo streaming.

**# Stati**

Numero di stati in cui è stato effettuato lo streaming.

**N. cluster**

Numero di elementi distinti [cluster](/help/AccountIQ/product-concepts.md#cluster-def) in cui è stato effettuato lo streaming.

**Intervallo geografico (miglia)**

La distanza massima tra le posizioni di streaming associate all’account.

**# AuthN OK**

Il numero di volte in cui gli utenti hanno effettuato l’accesso durante il periodo, utilizzando tale account.

**# AuthZ OK**

Numero di volte in cui un MVPD ha autorizzato un flusso o concesso l&#39;accesso (al contenuto) a tale account.

>[!NOTE]
>
>La **# AuthZ OK** è correlato al **N. richieste Play**; è più piccolo del **N. richieste Play** perché, ad Adobe, le autorizzazioni che vengono fornite per gli MVPD in genere per 24 ore.

**N. richieste Play**

Il numero effettivo di flussi durante il periodo di tempo.

**N. canali**

Numero totale di canali diversi che l&#39;account ha guardato nel periodo di tempo.

>[!NOTE]
>
>**N. canali** include i canali che non appartengono necessariamente al programmatore connesso.
>
>Questo numero per l&#39;account è stato visualizzato perché l&#39;account ha guardato il tuo canale, ma ha anche effettuato l&#39;accesso ad altri canali durante quel periodo di tempo.

**Pattern di utilizzo**

I numeri in questa colonna sono identificatori che corrispondono a uno dei 14 pattern con cui identifichiamo tutti gli account utente.

*Tabella: Identificatori del pattern di utilizzo nella mappatura CSV esportata con pattern di utilizzo*

| ID | 1 | 2 | 3 | 4 | 5 e 8 | 6 | 7 | 9 | 10 e 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Pattern di utilizzo | Utente regolare | Viaggiatore o pendolare | Famiglia grande | Chiudi familiari e amici | Condivisione di gruppi social | Grande gruppo di amici | Streaming simultaneo | Condivisione community | Comportamento incerto | Piccola famiglia | Seconda casa | Utilizzo anomalo |

{style=&quot;table-layout:auto&quot;}

**Probabilità di condivisione**

La probabilità di condivisione è la probabilità che l&#39;account specifico stia condividendo le proprie credenziali.

>[!NOTE]
>
> La media della probabilità di condivisione di tutti i conti (nel segmento selezionato) viene utilizzata per calcolare la [livello di condivisione](/help/AccountIQ/dashboard.md#sharing-level) del [Punteggio di condivisione aggregato](/help/AccountIQ/dashboard.md#aggregated-sharing).
