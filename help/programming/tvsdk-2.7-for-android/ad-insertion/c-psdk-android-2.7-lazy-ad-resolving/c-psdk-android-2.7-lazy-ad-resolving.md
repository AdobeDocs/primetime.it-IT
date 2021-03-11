---
description: La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per un utente in attesa dell'avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio.
keywords: Pigro;risoluzione annunci;Caricamento annunci
title: Lazy e risoluzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Panoramica {#lazy-ad-resolving}

La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per un utente in attesa dell&#39;avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio.

* Processo di risoluzione e caricamento degli annunci di base:

   1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
   1. TVSDK *carica* tutti gli annunci e li inserisce nella timeline.
   1. TVSDK sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.

   Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), assicura che il contenuto dell’annuncio sia in un formato che TVSDK può riprodurre e TVSDK inserisce gli annunci nella timeline. Questo processo di base di risoluzione e caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente che aspetta di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

* *Caricamento* annuncio pigro:

   1. TVSDK scarica una playlist e *risolve* tutti gli annunci.
   1. TVSDK *carica* annunci pre-scorrimento, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   1. TVSDK *carica* gli annunci rimanenti e li inserisce sulla timeline mentre si verifica la riproduzione.

   Questa funzione migliora il processo di base inserendo il lettore nello stato PREPARATO prima che tutti gli annunci vengano caricati.

* *Risoluzione* annunci pigri:

   1. TVSDK scarica la playlist.
   1. TVSDK risolve e carica tutti gli annunci pre-roll, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   1. TVSDK risolve e carica gli annunci rimanenti e li inserisce nella timeline mentre si verifica la riproduzione.

   Lazy Ad Resolving si basa su Lazy Ad Loading per consentire un avvio ancora più veloce. Una volta inseriti gli annunci pre-roll, TVSDK sposta il lettore nello stato PREPARATO, quindi risolve gli annunci aggiuntivi e li posiziona sulla timeline.

>[!IMPORTANT]
>
>Fattori da considerare con Lazy Ad Resolving:
>
>* La risoluzione degli annunci pigri è abilitata per impostazione predefinita. Se lo disattivi, tutti gli annunci vengono risolti prima dell’avvio della riproduzione.
>* Lazy Ad Resolving non consente la ricerca o il trickplay fino alla risoluzione di tutti gli annunci:

   >
   >    
   * Il lettore deve attendere l&#39;evento `kEventAdResolutionComplete` prima di consentire la ricerca o il gioco di trucco.
   >    * Se l’utente tenta di eseguire operazioni di ricerca o di trucco durante la risoluzione degli annunci, TVSDK genera l’errore `kECLazyAdResolutionInProgress`.
   >    * Se necessario, il lettore deve aggiornare la barra di scorrimento, *dopo* che ha ricevuto l&#39;evento `kEventAdResolutionComplete`.
>
>* Lazy Ad Resolving è solo per VOD. Non funzionerà con i flussi LIVE.
>* La funzione Lazy Ad Resolving non è compatibile con la funzione *Instant On* .

>
>  

Per ulteriori informazioni su Instant On, consulta l’ accesso immediato .
>
>* Mentre Lazy Ad Resolving consente di avviare la riproduzione molto più velocemente, se si verifica un&#39;interruzione pubblicitaria nei primi 60 secondi di riproduzione, potrebbe non essere risolto.
>* La risoluzione degli annunci pigri non influisce sugli annunci pre-roll.