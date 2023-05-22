---
description: TVSDK gestisce le sospensioni attività nei flussi video live e fornisce contenuto alternativo durante una sospensione attività.
title: Gestire le sospensioni attività
exl-id: 4a2ff371-69a9-4c13-ac61-3c5cd9c83a6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Gestire le sospensioni attività {#handle-blackouts}

TVSDK gestisce le sospensioni attività nei flussi video live e fornisce contenuto alternativo durante una sospensione attività.

Il caso d’uso più comune associato a una sospensione attività di programmazione è il caso in cui l’app del lettore fornisce contenuto alternativo agli utenti che non sono idonei a guardare il flusso principale. Questa app può utilizzare TVSDK per determinare l’inizio e la fine del periodo di sospensione attività. In questo modo, all&#39;inizio del periodo di sospensione, la riproduzione può passare dal flusso principale a uno alternativo e quindi tornare al flusso principale al termine del periodo di sospensione.

Per implementare la soluzione per questo caso d’uso:

1. Configura l&#39;app per abbonarti ai tag di sospensione attività in un manifesto live stream.

   TVSDK non è direttamente a conoscenza dei tag di sospensione attività, ma consente all’app di abbonarsi alle notifiche quando vengono rilevati tag specifici durante l’analisi del file manifesto.
1. Aggiungi un listener di notifica per `PTTimedMetadataChangedNotification`.

   Questa notifica viene inviata ogni volta che nel manifesto viene analizzato un tag sottoscritto e viene aggiunto un nuovo `PTTimedMetadata` è preparato da esso.

1. Implementare un metodo listener, ad esempio `onMediaPlayerSubscribedTagIdentified`, per `PTTimedMetadata` oggetti in primo piano.

1. Ogni volta che si verifica un aggiornamento durante la riproduzione, utilizzare `PTMediaPlayerTimeChangeNotification` listener da gestire `PTTimedMetadata` oggetti.

1. Aggiungi il `PTTimedMetadata` handler.

   Questo gestore consente di passare a un contenuto alternativo e tornare al contenuto principale come indicato dalla `PTTimedMetadata` e il tempo di riproduzione dell&#39;oggetto.

1. Utilizzare `onSubscribedTagInBackground` per implementare il metodo listener per `PTTimedMetadata` oggetti in background.

   Questo metodo monitora la temporizzazione del flusso in background, che consente di determinare quando è possibile tornare dal contenuto alternativo al contenuto principale.

1. Implementa un metodo listener per gli errori in background.
1. Se l&#39;intervallo di sospensione attività si trova nel DVR nel flusso di riproduzione, aggiornare gli intervalli non ricercabili.

   L&#39;applicazione deve impostare l&#39;intervallo non ricercabile nel DVR nei seguenti casi:

   * Quando si unisce lo streaming principale quando è presente una sospensione attività nel DVR.
   * Quando si torna al contenuto principale dal contenuto alternativo.
