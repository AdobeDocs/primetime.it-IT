---
description: TVSDK gestisce le blackout nei flussi video in diretta e fornisce contenuti alternativi durante una blackout.
title: Gestire i blackout
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# Gestire i blackout {#handle-blackouts}

TVSDK gestisce le blackout nei flussi video in diretta e fornisce contenuti alternativi durante una blackout.

Il caso d’uso più comune associato a un blackout di programmazione è quando l’app di lettore fornisce contenuto alternativo agli utenti che non sono idonei a guardare il flusso principale. Questa app può utilizzare TVSDK per determinare l’inizio e la fine del periodo di sospensione attività. In questo modo, all&#39;inizio del periodo di sospensione, la riproduzione può passare dal flusso principale a un flusso alternativo e quindi tornare al flusso principale quando il periodo di sospensione è terminato.

Per implementare la soluzione per questo caso d’uso:

1. Imposta l&#39;app per abbonarti ai tag di blackout in un manifesto di streaming live.

   TVSDK non è direttamente a conoscenza dei tag di blackout, ma consente all’app di abbonarsi alle notifiche quando si incontrano tag specifici durante l’analisi dei file manifest.
1. Aggiungi un listener di notifica per `PTTimedMetadataChangedNotification`.

   Questa notifica viene inviata ogni volta che un tag con sottoscrizione viene analizzato nel manifesto e ne viene preparato uno nuovo `PTTimedMetadata`.

1. Implementa un metodo listener, ad esempio `onMediaPlayerSubscribedTagIdentified`, per gli oggetti `PTTimedMetadata` in primo piano.

1. Ogni volta che si verifica un aggiornamento durante la riproduzione, utilizzare il listener `PTMediaPlayerTimeChangeNotification` per gestire gli oggetti `PTTimedMetadata`.

1. Aggiungi il gestore `PTTimedMetadata` .

   Questo gestore consente di passare al contenuto alternativo e di tornare al contenuto principale come indicato dall&#39;oggetto `PTTimedMetadata` e dal relativo tempo di riproduzione.

1. Utilizzare `onSubscribedTagInBackground` per implementare il metodo listener per gli oggetti `PTTimedMetadata` in background.

   Questo metodo controlla la tempistica del flusso in background, aiutando a determinare quando passare dal contenuto alternativo al contenuto principale.

1. Implementa un metodo listener per gli errori in background.
1. Se l&#39;intervallo di blackout si trova nel DVR del flusso di riproduzione, aggiornare gli intervalli non ricercabili.

   L&#39;applicazione deve impostare l&#39;intervallo non ricercabile nel DVR nei seguenti casi:

   * Quando si unisce al flusso principale quando un blackout è nel DVR.
   * Quando si torna al contenuto principale dal contenuto alternativo.