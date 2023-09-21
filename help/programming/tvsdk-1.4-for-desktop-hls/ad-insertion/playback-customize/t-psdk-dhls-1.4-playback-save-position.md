---
description: È possibile salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.
title: Salva la posizione del video e riprendi in un secondo momento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Salva la posizione del video e riprendi in un secondo momento{#save-the-video-position-and-resume-later}

È possibile salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.

Gli annunci inseriti in modo dinamico differiscono tra le sessioni utente, pertanto la posizione viene salvata **con** gli annunci uniti si riferiscono a una posizione diversa in una sessione futura. TVSDK fornisce metodi per recuperare la posizione di riproduzione ignorando gli annunci uniti.

1. Quando l’utente chiude un video, l’applicazione recupera e salva la posizione all’interno del video.

   >[!TIP]
   >
   >Le durate degli annunci non sono incluse.

   Le interruzioni pubblicitarie possono variare in ogni sessione a causa di modelli di annunci, limiti di frequenza e così via. L’ora corrente del video in una sessione potrebbe essere diversa in una sessione futura. Quando si salva una posizione nel video, l’applicazione recupera l’ora locale. Utilizza il `localTime` per leggere questa posizione , che puoi salvare sul dispositivo o in un database sul server.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Ad esempio, se l’utente si trova al 20° minuto del video e questa posizione include cinque minuti di annunci, `currentTime` will `be` 1200 secondi, mentre `localTime` in questa posizione `be` 900 secondi.

1. Ripristina la sessione utente quando l’attività del lettore riprende.

   TVSDK non riprende la riproduzione tra le inizializzazioni TVSDK perché non salva alcuna informazione localmente. L&#39;applicazione deve implementare questa logica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Per riprendere il video nella stessa posizione:

   * Per riprendere la riproduzione del video dalla posizione salvata da una sessione precedente, utilizzare `seekToLocal`.

     >[!TIP]
     >
     >Questo metodo viene chiamato solo con valori di ora locali. Se il metodo viene chiamato con i risultati dell&#39;ora corrente, si verifica un comportamento errato.

   * Per cercare fino all&#39;ora corrente, utilizzare `seek`.

1. Quando l&#39;applicazione riceve `onStatusChanged` evento di modifica dello stato, cerca nell’ora locale salvata.
1. Specifica le interruzioni pubblicitarie come specificato nell’interfaccia dei criteri relativi agli annunci.
1. Implementa un selettore di criteri per annunci personalizzato estendendo il selettore di criteri per annunci predefinito.
1. Fornisci le interruzioni pubblicitarie che devono essere presentate all&#39;utente implementando `selectAdBreaksToPlay`.

   Quando il lettore entra nello stato PREPARATO, tutti gli annunci sono già risolti, quindi il `AdPolicyInfo.adBreakTimelineItem` La proprietà contiene tutte le interruzioni pubblicitarie prima della posizione dell’ora locale. L’applicazione può decidere di riprodurre un’interruzione pubblicitaria pre-roll e riprendere all’ora locale specificata, riprodurre un’interruzione pubblicitaria mid-roll e riprendere all’ora locale specificata oppure non riprodurre interruzioni pubblicitarie.
