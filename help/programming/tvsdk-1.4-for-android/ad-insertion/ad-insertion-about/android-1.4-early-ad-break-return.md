---
description: Per l'inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un'interruzione di annuncio prima che tutti gli annunci nell'interruzione siano riprodotti al completamento.
seo-description: Per l'inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un'interruzione di annuncio prima che tutti gli annunci nell'interruzione siano riprodotti al completamento.
seo-title: Implementazione di un ritorno a capo rapido
title: Implementazione di un ritorno a capo rapido
uuid: 41b70ee1-290b-4732-899e-32b234ec1d9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementazione di un ritorno a capo rapido {#implement-an-early-ad-break-return}

Per l&#39;inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un&#39;interruzione di annuncio prima che tutti gli annunci nell&#39;interruzione siano riprodotti al completamento.

Ad esempio, la durata dell&#39;interruzione dell&#39;annuncio in alcuni eventi sportivi potrebbe non essere nota prima dell&#39;inizio dell&#39;interruzione. TVSDK fornisce una durata predefinita, ma se il gioco riprende prima del termine dell&#39;interruzione, è necessario uscire dall&#39;interruzione dell&#39;annuncio. Un altro esempio è rappresentato da un segnale di emergenza durante un&#39;interruzione pubblicitaria in un flusso live.

1. Iscriviti ai marcatori di annunci in uscita/in di giunzione ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`e `#EXT-X-CUE`).

   Per ulteriori informazioni su come unire marcatori di annunci in uscita/in, consultate Generatori di [opportunità e risolutori](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md)di contenuti.
1. Utilizzate un `ContentFactory`oggetto personalizzato.
1. In `retrieveGenerators()`, utilizza il `SpliceInPlacementOpportunityGenerator`.

   Ad esempio:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Per ulteriori informazioni sull&#39;uso di un&#39;app personalizzata `ContentFactory`, vedere il passaggio 1 in [Implementare un rilevatore](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) di opportunità personalizzato.

1. Sulla stessa personalizzazione `ContentFactory`, implementate `retrieveResolvers` e includete `AuditudeResolver` e `SpliceInCustomResolver`.

   Ad esempio:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

