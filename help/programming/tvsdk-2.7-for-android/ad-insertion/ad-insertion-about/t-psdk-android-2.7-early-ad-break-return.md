---
description: Per l’inserimento di annunci in streaming live, potrebbe essere necessario uscire da un’interruzione pubblicitaria prima che tutti gli annunci dell’interruzione vengano riprodotti fino al completamento.
title: Implementare un ritorno rapido dell’annuncio pubblicitario
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Implementare un ritorno rapido dell’annuncio pubblicitario  {#implement-an-early-ad-break-return}

Per l’inserimento di annunci in streaming live, potrebbe essere necessario uscire da un’interruzione pubblicitaria prima che tutti gli annunci dell’interruzione vengano riprodotti fino al completamento.

Ad esempio, la durata dell’interruzione pubblicitaria in alcuni eventi sportivi potrebbe non essere nota prima dell’inizio dell’interruzione. TVSDK fornisce una durata predefinita, ma se il gioco riprende prima del termine dell’interruzione, l’interruzione pubblicitaria deve essere chiusa. Un altro esempio è un segnale di emergenza durante un’interruzione pubblicitaria in un flusso live.

1. Iscriviti a `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, e `#EXT-X-CUE`, che rappresentano il giunto esterno/giunto nei marcatori.

   Per ulteriori informazioni su come montare i marcatori degli annunci in uscita/in, consulta [Generatori di opportunità e risolutori di contenuti](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md).

1. Utilizza un `ContentFactory`.
1. In entrata `retrieveGenerators`, utilizza `SpliceInPlacementOpportunityGenerator`.

   Ad esempio:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Per ulteriori informazioni sull&#39;utilizzo di un `ContentFactory`, vedere il passaggio 1 in [Implementare un generatore di opportunità personalizzato](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md).

1. Sulla stessa personalizzazione `ContentFactory`, implementare `retrieveResolvers` e includono `AuditudeResolver` e `SpliceInCustomResolver`.

   Ad esempio:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
