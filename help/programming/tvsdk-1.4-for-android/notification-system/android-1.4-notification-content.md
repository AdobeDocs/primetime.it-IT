---
description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.
title: Contenuto della notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---


# Contenuto della notifica {#notification-content}

Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.

L&#39;applicazione può recuperare la notifica e le informazioni sullo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

Implementa listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono notifiche di stato `MediaPlayerNotification`.

`MediaPlayerNotification` fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico delle notifiche `MediaPlayerNotification` . Ogni notifica contiene le seguenti informazioni:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFORMAZIONI, AVVERTENZA o ERRORE.
   * `code`: Una rappresentazione numerica della notifica.
   * `name`: Una descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: Coppie chiave/valore che contengono informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore corrispondente a un URL correlato alla notifica.

   * `innerNotification`: Riferimento a un altro  `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

Puoi archiviare queste informazioni localmente per analisi successive o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Imposta il sistema di notifica {#set-up-your-notification-system}

Puoi ascoltare le notifiche e aggiungere le tue notifiche personalizzate alla cronologia delle notifiche.

Il nucleo del sistema di notifica di Primetime Player è la classe `Notification` che rappresenta una notifica autonoma.

La classe `NotificationHistory` fornisce un meccanismo per l&#39;accumulo di notifiche. Memorizza un registro di oggetti di notifica (NotificationHistoryItem) che rappresenta un insieme di Notifiche.

Per ricevere le notifiche:

* Ascoltare notifiche
* Aggiungi notifiche alla cronologia delle notifiche

1. Ascoltare le modifiche allo stato.
1. Implementa il callback `MediaPlayer.PlaybackEventListener.onStateChanged` .
1. TVSDK passa due parametri al callback:

   * Il nuovo stato ( `MediaPlayer.PlayerState`)
   * Un oggetto `MediaPlayerNotification`

## Aggiungere registrazione e debug in tempo reale {#add-real-time-logging-and-debugging}

Puoi utilizzare le notifiche per implementare la registrazione in tempo reale nella tua applicazione video.

Il sistema di notifica ti consente di raccogliere informazioni di registrazione e debug per scopi diagnostici e di convalida senza che il sistema venga eccessivamente stressato.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non deve gestire il traffico ad alto carico. Se l’implementazione non deve essere completa, considera l’efficienza della trasmissione dei dati per evitare di sovraccaricare il sistema.

Ecco un esempio di come recuperare le notifiche.

1. Crea un thread di esecuzione basato su timer per l&#39;applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.

1. Se l&#39;intervallo del timer è troppo grande e le dimensioni dell&#39;elenco degli eventi sono troppo piccole, l&#39;elenco degli eventi di notifica si sovrapporrà. Per evitare questo overflow, effettuare una delle seguenti operazioni:

   * Diminuisce l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   * Aumenta le dimensioni dell’elenco delle notifiche.

1. Serializza le voci dell&#39;evento di notifica più recenti in formato JSON e invia le voci a un server remoto per la post-elaborazione.

   Il server remoto potrebbe quindi visualizzare graficamente i dati forniti in tempo reale.
1. Per rilevare la perdita degli eventi di notifica, cerca le lacune nella sequenza di valori di indice degli eventi.

   Ogni evento di notifica ha un valore di indice che viene incrementato automaticamente dalla classe `session.NotificationHistory`.

## Tag ID3 {#id-tags}

I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L’applicazione può estrarre dati dal tag .

>[!IMPORTANT]
>
>TVSDK riconosce i metadati ID3 (versione 2.3.0 o 2.4.0) nei flussi audio (AAC) e video (H.264), in qualsiasi codifica possibile (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora i tag ID3 che non sono in una delle versioni o dei formati riconosciuti. La codifica non specificata viene trattata come UTF8.

Quando TVSDK rileva i metadati ID3, invia una notifica con i seguenti dati:

* InfoCode = 303007
* TYPE = ID3
* NAME = non presente
* ID = 0

1. Implementa un listener di eventi per `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registralo con l&#39;oggetto `MediaPlayer` .

   TVSDK chiama questo listener quando rileva i metadati ID3.

   >[!NOTE]
   >
   >I suggerimenti per gli annunci personalizzati utilizzano lo stesso evento `onTimedMetadata` per indicare il rilevamento di un nuovo tag. Questo non deve causare confusione perché vengono rilevati suggerimenti di annunci personalizzati a livello di manifesto e i tag ID3 sono incorporati nel flusso. Per ulteriori informazioni, consulta custom-tags-configure .

1. Recupera i metadati.

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
