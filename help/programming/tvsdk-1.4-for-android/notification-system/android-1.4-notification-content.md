---
description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica nello stato del lettore.
seo-description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica nello stato del lettore.
seo-title: Contenuto notifica
title: Contenuto notifica
uuid: 89fb8f63-b0d5-45cd-bdad-348529fd07d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# Contenuto notifica {#notification-content}

Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica nello stato del lettore.

L’applicazione può recuperare le informazioni relative alla notifica e allo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

È possibile implementare i listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono notifiche di stato `MediaPlayerNotification`.

`MediaPlayerNotification` fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico delle notifiche `MediaPlayerNotification`. Ogni notifica contiene le informazioni seguenti:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFORMAZIONI, AVVISI O ERRORI.
   * `code`: Una rappresentazione numerica della notifica.
   * `name`: Descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: Coppie chiave/valore contenenti informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore che è un URL correlato alla notifica.

   * `innerNotification`: Un riferimento a un altro  `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

Potete archiviare queste informazioni localmente per un&#39;analisi successiva o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Configurare il sistema di notifica {#set-up-your-notification-system}

Potete ascoltare le notifiche e aggiungere notifiche personalizzate alla cronologia delle notifiche.

Il nucleo del sistema di notifica Primetime Player è la classe `Notification`, che rappresenta una notifica standalone.

La classe `NotificationHistory` fornisce un meccanismo per l&#39;accumulo di notifiche. Memorizza un registro di oggetti Notification (NotificationHistoryItem) che rappresenta un insieme di Notifiche.

Per ricevere le notifiche:

* Ascoltare le notifiche
* Aggiunta di notifiche alla cronologia delle notifiche

1. Ascoltare le modifiche allo stato.
1. Implementa il callback `MediaPlayer.PlaybackEventListener.onStateChanged`.
1. TVSDK passa due parametri al callback:

   * Il nuovo stato ( `MediaPlayer.PlayerState`)
   * Oggetto `MediaPlayerNotification`

## Aggiunta di registrazioni e debugging in tempo reale {#add-real-time-logging-and-debugging}

Potete utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.

Il sistema di notifica consente di raccogliere informazioni di registrazione e debug per la diagnostica e la convalida senza che il sistema venga eccessivamente stressato.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non deve gestire il traffico a carico elevato. Se non è necessario che l&#39;implementazione sia completa, considera l&#39;efficienza della trasmissione dei dati per evitare il sovraccarico del sistema.

Di seguito è riportato un esempio di come recuperare le notifiche.

1. Create un thread di esecuzione basato su timer per l’applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.

1. Se l&#39;intervallo del timer è troppo grande e le dimensioni dell&#39;elenco eventi sono troppo piccole, l&#39;elenco degli eventi di notifica si estenda. Per evitare questo overflow, effettuare una delle seguenti operazioni:

   * Diminuisce l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   * Aumentate la dimensione dell&#39;elenco delle notifiche.

1. Serializzare le voci dell&#39;evento di notifica più recente in formato JSON e inviare le voci a un server remoto per la post-elaborazione.

   Il server remoto potrebbe quindi visualizzare graficamente i dati forniti in tempo reale.
1. Per rilevare la perdita di eventi di notifica, cercate gli spazi vuoti nella sequenza di valori di indice dell&#39;evento.

   Ogni evento di notifica ha un valore di indice che viene incrementato automaticamente dalla classe `session.NotificationHistory`.

## Tag ID3 {#id-tags}

I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L&#39;applicazione può estrarre dati dal tag .

>[!IMPORTANT]
>
>TVSDK riconosce i metadati ID3 (versione 2.3.0 o 2.4.0) nei flussi audio (AAC) e video (H.264), in qualsiasi codifica possibile (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora i tag ID3 che non sono in una delle versioni o dei formati riconosciuti. La codifica non specificata viene trattata come UTF8.

Quando TVSDK rileva i metadati ID3, invia una notifica con i seguenti dati:

* InfoCode = 303007
* TYPE = ID3
* NAME = not present
* ID = 0

1. Implementare un listener di eventi per `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registrarlo con l&#39;oggetto `MediaPlayer`.

   TVSDK chiama questo listener quando rileva i metadati ID3.

   >[!NOTE]
   >
   >I suggerimenti per gli annunci personalizzati utilizzano lo stesso evento `onTimedMetadata` per indicare il rilevamento di un nuovo tag. Ciò non deve creare confusione perché vengono rilevati segnali pubblicitari personalizzati a livello di manifesto e i tag ID3 sono incorporati nel flusso. Per ulteriori informazioni, consultate custom-tags-configure .

1. Recuperate i metadati.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
