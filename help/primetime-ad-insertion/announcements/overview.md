---
title: Annunci di Adobe Primetime Ad Insertion
description: Annunci sulle ultime versioni di funzioni e altre notizie correlate su Primetime Ad Insertion
exl-id: 7d85d3a2-6786-47bd-8d45-ec162aea0ab3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Annunci Ad Insertion di Primetime

## Riduzione degli errori programmatici degli annunci tramite timeout per la risoluzione degli annunci

Pubblicato il 1 dicembre 2020

Adobe si concentra sull’aiutare i nostri clienti Ad Insertion di Primetime a massimizzare la monetizzazione del loro inventario di annunci. Prestiamo particolare attenzione alla riduzione della complessità di soddisfare la domanda programmatica, che rappresenta oltre tre quarti della spesa pubblicitaria digitale degli Stati Uniti secondo eMarketer. La vendita programmatica consente agli editori di massimizzare la domanda per il proprio inventario di annunci, aumentando i tassi di riempimento e il rendimento. Ma aumenta anche l’esposizione a errori pubblicitari come risposte VAST non corrette, errori HTTP e altri che possono portare a perdite di ricavi e/o esperienze visualizzatore inadeguate.

Un problema comune è rappresentato dalla lentezza e dalle risposte dei partner programmatici. In genere, le transazioni di annunci programmatici si verificano in millisecondi. Tuttavia, a volte una singola fonte di domanda può richiedere un tempo eccessivo per rispondere. Un ritardo da un singolo provider può influire sull’intero processo di realizzazione dell’annuncio, causando schermate vuote temporanee per il visualizzatore, spazi pubblicitari vuoti o, in casi estremi, la necessità di riavviare un flusso video. Sfortunatamente, identificare e aggirare le fonti di domanda lenta è una sfida importante.

Per risolvere questo problema, Adobe ha aggiunto nuovi strumenti all’Ad Insertion Primetime che consentono ai clienti di impostare vincoli di tempo per la risoluzione degli annunci. L’impostazione di queste regole fa sì che le origini di domanda lente vengano ignorate automaticamente, garantendo che i lettori video ricevano risposte pubblicitarie in modo tempestivo. Questo consente agli editori di limitare notevolmente le interruzioni da fonti di domanda lente, aiutandoli a massimizzare i tassi di riempimento dell’inventario e a fornire esperienze di visualizzazione ininterrotte e di qualità televisiva.

Per abilitare il timeout della risoluzione degli annunci in Primetime Ad Insertion, modifica le API di avvio per includere il parametro ptadtimeout (durata in millisecondi).  Eventuali richieste di annunci che non vengono completate prima della durata del timeout non verranno unite (verranno elaborati eventuali annunci di fallback).
