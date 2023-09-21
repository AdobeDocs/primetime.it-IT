---
description: La risoluzione e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente in attesa dell’avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio.
keywords: Lazy;Risoluzione annuncio;Caricamento annuncio
title: Risoluzione annuncio lazy
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Panoramica {#lazy-ad-resolving}

La risoluzione e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente in attesa dell’avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio.

* Processo di base di risoluzione e caricamento degli annunci:

   1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
   1. TVSDK *Carichi* tutti gli annunci e li inserisce nella timeline.
   1. TVSDK sposta il lettore nello stato READY e inizia la riproduzione del contenuto.

  Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), si assicura che il contenuto dell’annuncio sia in un formato riproducibile da TVSDK e che TVSDK inserisca gli annunci nella timeline. Questo processo di base di risoluzione e caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente in attesa di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

* *Caricamento annuncio lazy*:

   1. TVSDK scarica una playlist e *risolve* tutti gli annunci.
   1. TVSDK *Carichi* pre-roll di annunci, sposta il lettore nello stato READY e inizia la riproduzione del contenuto.
   1. TVSDK *Carichi* gli annunci rimanenti e li inserisce nella timeline durante la riproduzione.

  Questa funzione migliora il processo di base portando il lettore nello stato READY prima che tutti gli annunci vengano caricati.

* *Lazy Ad Resolving*:

   1. TVSDK scarica la playlist.
   1. TVSDK risolve e carica tutti gli annunci pre-roll, sposta il lettore nello stato READY e inizia la riproduzione del contenuto.
   1. TVSDK risolve e carica gli annunci rimanenti e li inserisce nella timeline quando si verifica la riproduzione.

  Lazy Ad Resolving si basa su Lazy Ad Loading per consentire un avvio ancora più rapido. Dopo che TVSDK inserisce qualsiasi annuncio pre-roll, sposta il lettore nello stato PREPARATO, quindi risolve gli annunci aggiuntivi e li posiziona sulla timeline.

>[!IMPORTANT]
>
>Fattori da considerare con Lazy Ad Resolving:
>
>* La funzione Lazy Ad Resolving è attivata per impostazione predefinita. Se lo disattivi, tutti gli annunci vengono risolti prima dell’inizio della riproduzione.
>* Lazy Ad Resolving non consente la ricerca o il trickplay fino a quando non vengono risolti tutti gli annunci:
>
>    * Il lettore deve attendere `kEventAdResolutionComplete` prima di consentire la ricerca o la riproduzione con trucco.
>    * Se l’utente tenta di eseguire operazioni di ricerca o di riproduzione tramite trucco mentre gli annunci sono ancora in fase di risoluzione, TVSDK genera il `kECLazyAdResolutionInProgress` errore.
>    * Se necessario, il lettore deve aggiornare la barra di scorrimento, *dopo* ricezione `kEventAdResolutionComplete` evento.
>
>* Lazy Ad Resolving è solo per VOD. Non funzionerà con i flussi LIVE.
>* Lazy Ad Resolving non è compatibile con *Istantanea attiva* funzionalità.
>
>  Per ulteriori informazioni su Instant On, vedere Instant-on.
>
>* Mentre la risoluzione dei Lazy Ad determina un avvio molto più rapido della riproduzione, se si verifica un’interruzione pubblicitaria nei primi 60 secondi di riproduzione, potrebbe non venire risolta.
>* La risoluzione lenta degli annunci non influisce sugli annunci pre-roll.
