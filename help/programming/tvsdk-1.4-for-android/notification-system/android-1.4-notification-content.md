---
description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche dello stato del lettore, avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche una modifica dello stato del lettore.
title: Contenuto della notifica
exl-id: b8298865-0389-4610-b495-b8735ef9cd56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Contenuto della notifica {#notification-content}

Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche dello stato del lettore, avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche una modifica dello stato del lettore.

L&#39;applicazione può recuperare le informazioni sulla notifica e sullo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

Puoi implementare i listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono `MediaPlayerNotification` notifiche di stato.

`MediaPlayerNotification` fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico di `MediaPlayerNotification` notifiche. Ogni notifica contiene le seguenti informazioni:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFO, WARN O ERROR.
   * `code`: rappresentazione numerica della notifica.
   * `name`: descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: coppie chiave/valore contenenti informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore che è un URL correlato alla notifica.

   * `innerNotification`: riferimento a un altro `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

È possibile archiviare queste informazioni in locale per un&#39;analisi successiva o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Configurare il sistema di notifica {#set-up-your-notification-system}

Puoi ascoltare le notifiche e aggiungere le tue notifiche alla cronologia delle notifiche.

Il nucleo del sistema di notifica del lettore Primetime è `Notification` che rappresenta una notifica autonoma.

Il `NotificationHistory` La classe fornisce un meccanismo per l&#39;accumulo di notifiche. Memorizza un registro di oggetti di notifica (NotificationHistoryItem) che rappresenta un insieme di notifiche.

Per ricevere le notifiche:

* Ascolta le notifiche
* Aggiungere notifiche alla cronologia delle notifiche

1. Ascolta le modifiche di stato.
1. Implementare `MediaPlayer.PlaybackEventListener.onStateChanged` callback.
1. TVSDK passa due parametri al callback:

   * Il nuovo stato ( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` oggetto

## Aggiungere registrazione in tempo reale e debug {#add-real-time-logging-and-debugging}

Puoi utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.

Il sistema di notifica consente di raccogliere le informazioni di registrazione e debug per la diagnostica e la convalida senza sovraccaricare il sistema.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non è previsto che gestisca il traffico con carichi elevati. Se l’implementazione non deve essere assolutamente completa, considera l’efficienza della trasmissione dei dati per evitare di sovraccaricare il sistema.

Di seguito è riportato un esempio di come recuperare le notifiche.

1. Crea un thread di esecuzione basato su timer per l’applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.

1. Se l&#39;intervallo del timer è troppo grande e la dimensione dell&#39;elenco eventi è troppo piccola, l&#39;elenco eventi di notifica verrà sottoposto a overflow. Per evitare questo overflow, eseguire una delle operazioni seguenti:

   * Diminuire l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   * Aumenta le dimensioni dell’elenco di notifiche.

1. Serializza le voci più recenti dell’evento di notifica in formato JSON e invia le voci a un server remoto per la post-elaborazione.

   Il server remoto potrebbe quindi visualizzare graficamente i dati forniti in tempo reale.
1. Per rilevare la perdita di eventi di notifica, cerca le lacune nella sequenza dei valori di indice degli eventi.

   Ogni evento di notifica ha un valore di indice che viene incrementato automaticamente da `session.NotificationHistory` classe.

## Tag ID3 {#id-tags}

I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell&#39;artista. TVSDK rileva i tag ID3 a livello del segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L’applicazione può estrarre dati dal tag.

>[!IMPORTANT]
>
>TVSDK riconosce i metadati ID3 (versione 2.3.0 o 2.4.0) nei flussi audio (AAC) e video (H.264), in una qualsiasi delle sue possibili codifiche (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora i tag ID3 che non sono in una delle versioni o dei formati riconosciuti. La codifica non specificata viene trattata come UTF8.

Quando TVSDK rileva i metadati ID3, invia una notifica con i seguenti dati:

* InfoCode = 303007
* TYPE = ID3
* NAME = non presente
* ID = 0

1. Implementare un listener di eventi per `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registrarlo con il `MediaPlayer` oggetto.

   TVSDK chiama questo listener quando rileva i metadati ID3.

   >[!NOTE]
   >
   >I suggerimenti degli annunci personalizzati utilizzano lo stesso `onTimedMetadata` per indicare il rilevamento di un nuovo tag. Ciò non dovrebbe causare confusione perché vengono rilevati suggerimenti di annunci personalizzati a livello del manifesto e i tag ID3 sono incorporati nel flusso. Per ulteriori informazioni, consulta custom-tags-configure .

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
