---
title: Limitazioni e problemi noti
description: Problemi noti nel prodotto.
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Problemi noti e limitazioni {#known-issues}

Adobe si impegna a offrire funzionalità affidabili ed esperienze utente senza soluzione di continuità attraverso le sue offerte. La versione corrente (versione 1.0) di Account IQ fornisce analisi di condivisione di utilizzo e abbonamento ai provider di streaming con un elevato grado di affidabilità. Tuttavia, le seguenti limitazioni saranno applicate nelle prossime versioni.

* Quando si definiscono le coorti nelle pagine del dashboard o dei rapporti, al momento non è possibile aggiungere metriche quali **numero di dispositivi** per perfezionare il segmento. Questa funzionalità sarà disponibile in una versione futura.

* Quando si stimano i punteggi di condivisione per i singoli account, Account IQ adotta un approccio conservativo che consente alle aziende di agire sulla condivisione con grande fiducia. Tuttavia, questo approccio tende a sottovalutare l&#39;ammontare totale della condivisione quando aggregata tra più account.

* La [Punteggio di condivisione generale](/help/AccountIQ/dashboard.md#overall-sharing-score) attualmente solo i fattori [Livello di condivisione](/help/AccountIQ/dashboard.md#sharing-level) e [Utilizzo dagli account condivisi](/help/AccountIQ/dashboard.md#usage-from-shared-accounts). Le versioni future includeranno metriche aggiuntive.

* Quando definisci le coorti nella dashboard o nelle pagine dei report, i selettori per MVPD e canali non dispongono al momento del meccanismo di ricerca.

* Quando si definiscono le coorti nelle pagine del dashboard o dei report, è previsto un limite per selezionare solo fino a 10 MVPD e programmatori (o singoli canali).

* Attualmente, la possibilità di esportare statistiche sui conti è limitata all&#39;esportazione di 1000 conti.

* Opzione da selezionare [Tipo di segmento](#segment-type) quando si definiscono le operazioni, è possibile **Numero fisso di account**. La **Numero di conti variabili** Sarà disponibile in una versione successiva.

* Le sezioni Benchmarking, Detection Models, Segments, SnSnapshot e Rules nella navigazione a sinistra sono attualmente disabilitate e saranno disponibili in una versione successiva.

* Durante la creazione [Operazioni](/help/AccountIQ/operation-affecting-user-segment.md), è possibile identificare solo due tipi [Azioni](/help/AccountIQ/operation-affecting-user-segment.md) a partire da ora — Regole di controllo della concorrenza e azioni esterne.

* Attualmente, è possibile creare solo le operazioni e [programmato](/help/AccountIQ/operation-affecting-user-segment.md#action). Le versioni future ti consentiranno di fermarle, riprenderle e gestirle completamente.

* A causa del set più limitato di dati utilizzati, la modalità di isolamento non riflette realmente la quantità di condivisione. Pertanto, MVPD in modalità Isolamento non può essere confrontato con qualsiasi altro MVPD. <!--do we need to separate out this limitation, which is from a different persona i.e. only for Programmer persona?-->

* Quando definisci un nuovo [segmento](/help/AccountIQ/segments-timeframe.md) per un’operazione puoi aggiungere metriche. Ma se selezioni un segmento salvato non puoi aggiungere altre metriche per perfezionarlo.

* Il selettore della granularità e dell’intervallo temporale è limitato a una settimana o un mese, il che significa che i dati possono essere valutati solo in una settimana o un mese.

* Gli intervalli predefiniti sono attualmente disabilitati in modalità granularità e selettore dell’intervallo di tempo e saranno disponibili in una versione futura.
