---
description: TVSDK gestisce i blackout nei flussi video live e fornisce contenuto alternativo durante un blackout.
seo-description: TVSDK gestisce i blackout nei flussi video live e fornisce contenuto alternativo durante un blackout.
seo-title: Gestione dei blackout nei flussi live
title: Gestione dei blackout nei flussi live
uuid: 1f70a272-bc77-4d41-a999-b076cb42ac5e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Gestione dei blackout nei flussi live{#handle-blackouts-in-live-streams}

TVSDK gestisce i blackout nei flussi video live e fornisce contenuto alternativo durante un blackout.

Il caso d’uso più comune associato a un blackout di programmazione è quando l’app lettore fornisce contenuto alternativo agli utenti che non possono guardare il flusso principale. Questa app può utilizzare TVSDK per determinare l&#39;inizio e la fine del periodo di blackout. In questo modo, all&#39;inizio del periodo di blackout, la riproduzione può passare dal flusso principale a un flusso alternativo e quindi tornare al flusso principale al termine del periodo di blackout.

Per implementare la soluzione per questo caso di utilizzo:

1. Configurate l&#39;app per iscrivervi ai tag blackout in un manifesto del flusso live.

   TVSDK non è direttamente a conoscenza dei tag di blackout, ma consente all&#39;app di abbonarsi alle notifiche quando vengono riscontrati tag specifici durante l&#39;analisi dei file manifest.
1. Aggiungete un listener di notifica per `PTTimedMetadataChangedNotification`.

   Questa notifica viene inviata ogni volta che un tag sottoscritto viene analizzato nel manifesto e da esso `PTTimedMetadata` viene preparato un nuovo tag.

1. Implementare un metodo listener, ad esempio `onMediaPlayerSubscribedTagIdentified`, per `PTTimedMetadata` gli oggetti in primo piano.

1. Ogni volta che si verifica un aggiornamento durante la riproduzione, utilizzare il `PTMediaPlayerTimeChangeNotification` listener per gestire `PTTimedMetadata` gli oggetti.

1. Aggiungete il `PTTimedMetadata` gestore.

   Questo gestore consente di passare al contenuto alternativo e di tornare al contenuto principale come indicato dall&#39; `PTTimedMetadata` oggetto e dal relativo tempo di riproduzione.

1. Utilizzare `onSubscribedTagInBackground` per implementare il metodo listener per `PTTimedMetadata` gli oggetti in background.

   Questo metodo controlla il tempo nel flusso di sfondo, consentendo di determinare quando passare dal contenuto alternativo al contenuto principale.

1. Implementare un metodo listener per gli errori in background.
1. Se l’intervallo di blackout è nel DVR sul flusso di riproduzione, aggiornate gli intervalli non ricercabili.

   L&#39;applicazione deve impostare l&#39;intervallo non ricercabile nel DVR nei seguenti casi:

   * Quando si unisce al flusso principale quando un blackout è nel DVR.
   * Quando si ritorna al contenuto principale dal contenuto alternativo.

