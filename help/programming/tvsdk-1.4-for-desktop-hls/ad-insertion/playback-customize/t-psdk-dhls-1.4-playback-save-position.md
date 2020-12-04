---
description: Potete salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.
seo-description: Potete salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.
seo-title: Salvate la posizione del video e riprendete più tardi
title: Salvate la posizione del video e riprendete più tardi
uuid: 03ed5c63-008d-4dd1-9a31-baefa73b56e2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Salvate la posizione del video e riprendete più tardi{#save-the-video-position-and-resume-later}

Potete salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.

Gli annunci inseriti dinamicamente differiscono tra le sessioni utente, pertanto il salvataggio della posizione **con** annunci con giunzione a coppie fa riferimento a una posizione diversa in una sessione futura. TVSDK fornisce metodi per recuperare la posizione di riproduzione ignorando gli annunci in sequenza.

1. Quando l’utente esce da un video, l’applicazione recupera e salva la posizione nel video.

   >[!TIP]
   >
   >Le durate degli annunci non sono incluse.

   Le interruzioni di annuncio possono variare in ogni sessione a causa di pattern di annunci, limiti di frequenza e così via. L’ora corrente del video in una sessione potrebbe essere diversa in una sessione futura. Quando si salva una posizione nel video, l&#39;applicazione recupera l&#39;ora locale . Utilizzare la proprietà `localTime` per leggere questa posizione, che è possibile salvare sul dispositivo o in un database sul server.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Ad esempio, se l&#39;utente si trova al 20° minuto del video e questa posizione include cinque minuti di annunci, `currentTime` sarà `be` 1200 secondi, mentre `localTime` a questa posizione `be` 900 secondi.

1. Ripristinare la sessione utente quando l&#39;attività del lettore riprende.

   TVSDK non riprende la riproduzione tra le inizializzazioni TVSDK perché non salva informazioni localmente. L&#39;applicazione deve implementare questa logica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Per riprendere il video nella stessa posizione:

   * Per riprendere la riproduzione del video dalla posizione salvata da una sessione precedente, utilizzate `seekToLocal`.

      >[!TIP]
      >
      >Questo metodo viene chiamato solo con valori di ora locali. Se il metodo viene chiamato con i risultati dell&#39;ora corrente, si verifica un comportamento non corretto.

   * Per cercare l&#39;ora corrente, utilizzare `seek`.

1. Quando l&#39;applicazione riceve l&#39;evento di modifica dello stato `onStatusChanged`, cercare l&#39;ora locale salvata.
1. Specifica le interruzioni di annuncio come specificato nell&#39;interfaccia dei criteri di annuncio.
1. Implementa un selettore di criteri di annunci personalizzato estendendo il selettore di criteri di annunci predefinito.
1. Fornite le interruzioni pubblicitarie che devono essere presentate all&#39;utente implementando `selectAdBreaksToPlay`.

   Quando il lettore inserisce lo stato PREPARATO, tutti gli annunci sono già risolti, quindi la proprietà `AdPolicyInfo.adBreakTimelineItem` contiene tutte le interruzioni di annuncio prima della posizione dell&#39;ora locale. L&#39;applicazione può decidere di riprodurre un&#39;interruzione di annuncio pre-roll e riprendere fino all&#39;ora locale specificata, di riprodurre un&#39;interruzione di annuncio mid-roll e riprendere fino all&#39;ora locale specificata, o di non riprodurre interruzioni di annuncio.
