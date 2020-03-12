---
description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
seo-description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
seo-title: Considerazioni e procedure ottimali
title: Considerazioni e procedure ottimali
uuid: a65c9739-ed83-4519-8ae5-7ba4c8f1ca49
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Considerazioni e procedure ottimali {#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Ricorda le seguenti informazioni quando utilizzi TVSDK:

* Adobe Primetime non funziona sui simulatori iOS.

   Per eseguire il test dovete utilizzare dei dispositivi reali.

* La riproduzione è supportata solo per il contenuto HTTP Live Streaming (HLS).

* Il contenuto video principale può essere multiplexato, dove i flussi video e audio si trovano nella stessa rappresentazione, o non multiplexato, dove i flussi video e audio si trovano in rappresentazioni separate.

* L&#39;API TVSDK è implementata in Objective-C.

* La riproduzione video richiede il framework nativo di Apple AV Foundation. Questo incide su come e quando è possibile accedere alle risorse multimediali, inclusi sottotitoli e timeline codificati:

   * Le regolazioni della timeline non possono essere riviste dopo la configurazione iniziale.

      Ad esempio, un annuncio non può essere rimosso dalla timeline dopo che è stato riprodotto. Se l’utente tenta di tornare alla presentazione, lo stesso annuncio viene riprodotto anche se il criterio avrebbe dovuto rimuovere l’annuncio.

   * A seconda della precisione del codificatore, la durata effettiva del supporto codificato potrebbe essere diversa dalle durate registrate nel manifesto della risorsa di flusso.

      Non esiste un modo affidabile per risincronizzare tra la timeline virtuale ideale e la timeline di riproduzione effettiva. Il tracciamento dell’avanzamento della riproduzione del flusso per la gestione degli annunci e per l’analisi video deve utilizzare il tempo di riproduzione effettivo, pertanto il comportamento dei rapporti e dell’interfaccia utente potrebbe non tenere traccia con precisione dei contenuti multimediali e pubblicitari.

   * L’agente utente in entrata per tutte le richieste HTTP da TVSDK su questa piattaforma è determinato dal dispositivo e dalla versione iOS in esecuzione sul dispositivo.

      Per impostazione predefinita, il valore della stringa agente utente corrisponde a quello assegnato dal sistema operativo.

## Best practice {#section_tvsdk_best_practices}

Seguono alcune pratiche consigliate per TVSDK:

* Utilizzate HLS versione 3.0 o successiva per il contenuto del programma.

* Utilizzate lo strumento MediaReamvalidator di Apple per convalidare i flussi VOD.

* La classe PTSDKConfig fornisce metodi per applicare SSL alle richieste effettuate ai server Primetime ad determinata, DRM e Video Analytics.

Per ulteriori informazioni, vedere i metodi forceHTTPS e isForcingHTTPS in questa classe.

[!IMPORTANT]

Le richieste inviate a domini di terze parti, quali Pixel di tracciamento annunci, URL di contenuti e annunci e richieste simili, non vengono modificate. È responsabilità dei fornitori di contenuti e dei server di annunci fornire URL supportati tramite HTTPS.