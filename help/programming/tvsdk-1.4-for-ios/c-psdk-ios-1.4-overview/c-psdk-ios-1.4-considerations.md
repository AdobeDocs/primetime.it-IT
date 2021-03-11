---
description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
title: Considerazioni e best practice
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Considerazioni e best practice{#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Quando utilizzi TVSDK, tieni presente le seguenti informazioni:

* Adobe Primetime non funziona sui simulatori iOS.

   Devi utilizzare dispositivi reali per il test.
* La riproduzione è supportata solo per i contenuti HTTP Live Streaming (HLS).
* Il contenuto video principale può essere multiplexato, dove i flussi video e audio si trovano nella stessa rappresentazione, o non multiplexato, dove i flussi video e audio si trovano in rappresentazioni separate.
* L’API TVSDK è implementata in Objective-C.
* La riproduzione video richiede il framework nativo di Apple AV Foundation. Questo influisce su come e quando è possibile accedere alle risorse multimediali, inclusi i sottotitoli e le timeline, :

   * Le regolazioni della timeline non possono essere riviste dopo la configurazione iniziale.

      Ad esempio, un annuncio non può essere rimosso dalla timeline dopo la riproduzione. Se l’utente cerca di nuovo nella presentazione, lo stesso annuncio viene riprodotto anche se il criterio sarebbe stato quello di rimuovere l’annuncio.
   * A seconda della precisione del codificatore, la durata effettiva del contenuto multimediale codificato potrebbe differire dalle durate registrate nel manifesto della risorsa di flusso.

      Non esiste un modo affidabile per eseguire la risincronizzazione tra la timeline virtuale ideale e la timeline effettiva di riproduzione. Il tracciamento dell’avanzamento della riproduzione in streaming per la gestione degli annunci e Video Analytics deve utilizzare il tempo di riproduzione effettivo, pertanto il comportamento di reporting e interfaccia utente potrebbe non tenere traccia con precisione del contenuto multimediale e pubblicitario.
   * L’agente utente in entrata per tutte le richieste HTTP da TVSDK su questa piattaforma è determinato dal dispositivo e dalla versione iOS in esecuzione sul dispositivo.

      Il valore della stringa dell&#39;agente utente viene impostato automaticamente su quello che il sistema operativo assegna.

## Best practice {#section_tvsdk_best_practices}

Di seguito sono riportate le pratiche consigliate per TVSDK:

* Utilizza HLS versione 3.0 o successiva per il contenuto del programma.
* Utilizza lo strumento mediastreamvalidator di Apple per convalidare i flussi VOD.
* La classe `PTSDKConfig` fornisce metodi per applicare SSL alle richieste effettuate ai server Primetime ad decision ioning, DRM e Video Analytics.

   Per ulteriori informazioni, vedere i metodi `forceHTTPS` e `isForcingHTTPS` in questa classe.

   >[!IMPORTANT]
   >
   >Le richieste a domini di terze parti come pixel di tracciamento annunci, URL di contenuti e annunci e richieste simili non vengono modificate. È responsabilità dei provider di contenuti e dei server di annunci fornire URL supportati tramite HTTPS.

