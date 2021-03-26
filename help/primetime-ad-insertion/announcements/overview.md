---
title: Annunci Adobe Primetime Ad Insertion
description: Annunci su nuove versioni e altre notizie correlate su Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: d8fde0d03bea85b3fefcfa5dcbfddee76b17de03
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Annunci di Primetime Ad Insertion

## Riduzione degli errori programmatici degli annunci tramite timeout della risoluzione degli annunci

Pubblicato il 1° dicembre 2020

Adobe si concentra sull’aiutare i clienti di Primetime Ad Insertion a massimizzare la monetizzazione del proprio ad inventory. Prestiamo particolare attenzione alla riduzione delle complessità di soddisfare la domanda programmatica, che rappresenta oltre tre quarti della spesa pubblicitaria digitale statunitense secondo eMarketing. La vendita programmatica consente agli editori di massimizzare la domanda per il proprio inventario pubblicitario, portando a tassi di riempimento e rendimento più elevati. Ma aumenta anche l&#39;esposizione a errori di annunci come risposte VAST malformate, errori HTTP e altri che possono portare alla perdita di entrate e/o a esperienze di visualizzatori scadenti.

Un problema comune sono le risposte lente degli annunci da parte dei partner programmatici. In genere, le transazioni degli annunci programmatici si verificano in millisecondi. Tuttavia, a volte una singola fonte di domanda può richiedere un tempo eccessivo per rispondere. Un ritardo da un singolo provider può influire sull&#39;intero processo di evasione degli annunci, causando schermate vuote temporanee per il visualizzatore, slot per annunci non compilati o, in casi estremi, la necessità di riavviare un flusso video. Sfortunatamente, identificare e aggirare le fonti di domanda lente è una sfida importante.

Per risolvere questo problema, Adobe ha aggiunto nuovi strumenti a Primetime Ad Insertion che consentono ai clienti di impostare limiti di tempo per la risoluzione degli annunci. L&#39;impostazione di queste regole fa sì che le fonti di domanda lenta vengano ignorate automaticamente, garantendo che i lettori video ricevano le risposte degli annunci in modo tempestivo. Questo consente agli editori di limitare notevolmente le interruzioni da fonti a bassa domanda, aiutandoli a massimizzare i tassi di riempimento delle scorte e a fornire esperienze di visualizzazione ininterrotte e di qualità televisiva.

Per abilitare il timeout della risoluzione degli annunci in Primetime Ad Insertion, modifica le API di bootstrap in modo da includere il parametro ptadtimeout (durata in millisecondi).  Eventuali richieste di annunci che non vengono completate prima della durata del timeout non verranno unite (verranno elaborati eventuali annunci di fallback).