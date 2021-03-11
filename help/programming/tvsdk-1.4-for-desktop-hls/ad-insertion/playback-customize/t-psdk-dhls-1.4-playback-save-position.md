---
description: È possibile salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.
title: Salva la posizione del video e riprendi più tardi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# Salva la posizione del video e riprendi più tardi{#save-the-video-position-and-resume-later}

È possibile salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.

Gli annunci inseriti in modo dinamico differiscono tra le sessioni utente, pertanto il salvataggio della posizione **con** annunci uniti fa riferimento a una posizione diversa in una sessione futura. TVSDK fornisce metodi per recuperare la posizione di riproduzione ignorando gli annunci in sequenza.

1. Quando l&#39;utente chiude un video, l&#39;applicazione recupera e salva la posizione nel video.

   >[!TIP]
   >
   >Le durate degli annunci non sono incluse.

   Le interruzioni di annunci possono variare in ogni sessione a causa di pattern di annunci, limiti di frequenza e così via. L&#39;ora corrente del video in una sessione potrebbe essere diversa in una sessione futura. Quando si salva una posizione nel video, l&#39;applicazione recupera l&#39;ora locale . Utilizza la proprietà `localTime` per leggere questa posizione , che puoi salvare sul dispositivo o in un database sul server.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Ad esempio, se l’utente si trova al 20° minuto del video e questa posizione include cinque minuti di annunci, `currentTime` `be` sarà di  1200 secondi, mentre `localTime` in questa posizione sarà di `be` 900 secondi.

1. Ripristina la sessione utente quando riprende l’attività del lettore.

   TVSDK non riprende la riproduzione tra le inizializzazioni TVSDK perché non salva alcuna informazione localmente. L’applicazione deve implementare questa logica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Per riprendere il video nella stessa posizione:

   * Per riprendere la riproduzione del video dalla posizione salvata da una sessione precedente, utilizza `seekToLocal`.

      >[!TIP]
      >
      >Questo metodo viene chiamato solo con valori di ora locali. Se il metodo viene chiamato con i risultati dell&#39;ora corrente, si verifica un comportamento errato.

   * Per cercare l&#39;ora corrente, utilizza `seek`.

1. Quando l&#39;applicazione riceve l&#39;evento di modifica dello stato `onStatusChanged`, cerca l&#39;ora locale salvata.
1. Fornisci le interruzioni pubblicitarie come specificato nell&#39;interfaccia dei criteri per gli annunci.
1. Implementa un selettore di criteri di annunci personalizzato estendendo il selettore di criteri di annunci predefinito.
1. Fornisci le interruzioni pubblicitarie che devono essere presentate all&#39;utente implementando `selectAdBreaksToPlay`.

   Quando il lettore inserisce lo stato PREPARATO, tutti gli annunci sono già risolti, pertanto la proprietà `AdPolicyInfo.adBreakTimelineItem` contiene tutte le interruzioni di annunci prima della posizione dell&#39;ora locale. L&#39;applicazione può decidere di riprodurre un annuncio pre-roll e riprendere all&#39;ora locale specificata, riprodurre un&#39;interruzione pubblicitaria mid-roll e riprendere all&#39;ora locale specificata, o riprodurre senza interruzioni pubblicitarie.
