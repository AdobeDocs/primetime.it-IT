---
description: La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente che attende l’avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio.
keywords: Lazy;Ad resolving;Ad loading
seo-description: La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente che attende l’avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio.
seo-title: Lazy e risoluzione
title: Lazy e risoluzione
uuid: cf9ba788-b83f-43aa-94c4-db391d92a77b
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Panoramica {#lazy-ad-resolving}

La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente che attende l’avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio.

* Processo di base per la risoluzione e il caricamento degli annunci:

   1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
   1. TVSDK *carica* tutti gli annunci e li inserisce nella timeline.
   1. TVSDK sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.

   Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), assicura che il contenuto dell’annuncio sia in un formato che possa essere riprodotto da TVSDK e che TVSDK inserisca gli annunci nella timeline. Questo processo di base per la risoluzione e il caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente che attende di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

* *Caricamento* annuncio non aggiornato:

   1. TVSDK scarica una playlist e *risolve* tutti gli annunci.
   1. TVSDK *carica* annunci pre-roll, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   1. TVSDK *carica* gli annunci rimanenti e li inserisce nella timeline durante la riproduzione.

   Questa funzione migliora il processo di base mettendo il lettore nello stato PREPARATO prima che tutti gli annunci vengano caricati.

* *Lazy Ad Resolving*:

   1. TVSDK scarica la playlist.
   1. TVSDK risolve e carica eventuali annunci pre-roll, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   1. TVSDK risolve e carica gli annunci rimanenti e li inserisce sulla timeline durante la riproduzione.

   Lazy Ad Resolving si basa su Lazy Ad Loading per consentire un avvio ancora più rapido. Dopo che TVSDK ha inserito qualsiasi annuncio pre-roll, sposta il lettore nello stato PREPARED, quindi risolve annunci aggiuntivi e li inserisce nella timeline.

>[!IMPORTANT]
>
>Fattori da considerare con Lazy Ad Resolving:
>
>* Lazy Ad Resolving è attivato per impostazione predefinita. Se lo disattivate, tutti gli annunci vengono risolti prima dell&#39;avvio della riproduzione.
>* Lazy Ad Resolving non consente la ricerca o il trickplay fino alla risoluzione di tutti gli annunci:

   >
   >    
   * Il lettore deve attendere l&#39; `kEventAdResolutionComplete` evento prima di consentire la ricerca o il gioco di trucco.
   >    * Se l’utente tenta di eseguire operazioni di ricerca o di riproduzione ingannevole durante la risoluzione degli annunci, TVSDK genera l’ `kECLazyAdResolutionInProgress` errore.
   >    * Se necessario, il lettore deve aggiornare la barra di scorrimento, *dopo* la ricezione dell’ `kEventAdResolutionComplete` evento.
>
>* Lazy Ad Resolving è solo per VOD. Non funzionerà con i flussi LIVE.
>* Lazy Ad Resolving è incompatibile con la funzione *Instant On* .

>
>  

Per ulteriori informazioni su Instant On, consultate instant-on .
>
>* Mentre la funzione Lazy Ad Resolving consente di avviare la riproduzione molto più rapidamente, se si verifica un&#39;interruzione pubblicitaria nei primi 60 secondi di riproduzione, potrebbe non essere stata risolta.
>* La risoluzione degli annunci pigri non influisce sugli annunci pre-roll.