---
title: ' Annunci Adobe Primetime  Ad Insertion'
seo-title: ' Annunci Adobe Primetime  Ad Insertion'
description: Annunci sulle ultime novità su Primetime  Ad Insertion
seo-description: Annunci sulle ultime novità su Primetime  Ad Insertion
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Annunci Primetime  Ad Insertion

## Riduzione degli errori programmatici degli annunci tramite timeout della risoluzione degli annunci

Pubblicato il 1° dicembre 2000

 Adobe è incentrato sull&#39;aiuto ai nostri clienti Ad Insertion  Primetime per massimizzare la monetizzazione del loro inventario pubblicitario. Prestiamo particolare attenzione alla riduzione della complessità di soddisfare la domanda programmatica, che rappresenta oltre i tre quarti delle spese di video digitali statunitensi e spese secondo eMarketer. La vendita programmatica consente agli editori di massimizzare la domanda per il proprio inventario pubblicitario, portando a tassi di riempimento e di rendimento più elevati. Ma aumenta anche l&#39;esposizione a errori di annunci come risposte VAST errate, errori HTTP e altri che possono portare a perdite di entrate e/o a esperienze di visualizzazione scadenti.

Un problema comune è rappresentato dalla lentezza delle risposte fornite dai partner programmatici. In genere, le transazioni di annunci programmatici si verificano in millisecondi. Tuttavia, a volte una singola origine della domanda potrebbe richiedere un tempo eccessivo per rispondere. Un ritardo da un singolo fornitore può influenzare l&#39;intero processo di evasione degli annunci, causando schermate vuote temporanee per il visualizzatore, slot per annunci non compilati o, in casi estremi, la necessità di riavviare un flusso video. Sfortunatamente, identificare e bypassare le fonti di domanda lente è una sfida importante.

Per risolvere questo problema,  Adobe ha aggiunto nuovi strumenti al Ad Insertion Primetime  che consentono ai clienti di impostare limiti di tempo per la risoluzione degli annunci. Impostando queste regole, le fonti di domanda lenta vengono ignorate automaticamente, garantendo che i lettori video ricevano le risposte degli annunci in modo tempestivo. Questo consente agli editori di limitare notevolmente le interruzioni da fonti di domanda lente, aiutandoli a ottimizzare i tassi di riempimento delle scorte e a fornire esperienze di visualizzazione ininterrotte e di qualità televisiva.

Per abilitare il timeout di risoluzione degli annunci in Primetime  Ad Insertion, modificate le API di avvio in modo da includere il parametro ptadtimeout (durata in millisecondi).  Eventuali richieste di annunci che non vengono completate prima della durata di timeout non verranno cucite (eventuali annunci di fallback verranno elaborati).