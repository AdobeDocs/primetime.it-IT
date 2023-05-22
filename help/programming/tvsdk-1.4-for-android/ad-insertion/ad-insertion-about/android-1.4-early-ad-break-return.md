---
description: Per l’inserimento di annunci in streaming live, potrebbe essere necessario uscire da un’interruzione pubblicitaria prima che tutti gli annunci dell’interruzione vengano riprodotti fino al completamento.
title: Implementare un ritorno rapido dell’annuncio pubblicitario
exl-id: 38386ab7-0e3b-4628-84eb-470d585eb929
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# Implementare un ritorno rapido dell’annuncio pubblicitario {#implement-an-early-ad-break-return}

Per l’inserimento di annunci in streaming live, potrebbe essere necessario uscire da un’interruzione pubblicitaria prima che tutti gli annunci dell’interruzione vengano riprodotti fino al completamento.

Ad esempio, la durata dell’interruzione pubblicitaria in alcuni eventi sportivi potrebbe non essere nota prima dell’inizio dell’interruzione. TVSDK fornisce una durata predefinita, ma se il gioco riprende prima del termine dell’interruzione, l’interruzione pubblicitaria deve essere chiusa. Un altro esempio è un segnale di emergenza durante un’interruzione pubblicitaria in un flusso live.

1. Iscriviti ai marcatori degli annunci in uscita/in del giunto ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, e `#EXT-X-CUE`).

   Per ulteriori informazioni su come montare i marcatori degli annunci in uscita/in, consulta [Generatori di opportunità e risolutori di contenuti](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md).
1. Utilizza un `ContentFactory`.
1. In entrata `retrieveGenerators()`, utilizza `SpliceInPlacementOpportunityGenerator`.

   Ad esempio:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Per ulteriori informazioni sull&#39;utilizzo di un `ContentFactory`, vedere il passaggio 1 in [Implementare un rilevatore di opportunità personalizzato](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) .

1. Sulla stessa personalizzazione `ContentFactory`, implementare `retrieveResolvers` e includono `AuditudeResolver` e `SpliceInCustomResolver`.

   Ad esempio:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
