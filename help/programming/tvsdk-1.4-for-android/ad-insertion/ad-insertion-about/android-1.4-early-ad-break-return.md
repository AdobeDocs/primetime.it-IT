---
description: Per l'inserimento di annunci in streaming live, potrebbe essere necessario uscire da un'interruzione pubblicitaria prima che tutti gli annunci nell'interruzione siano riprodotti al completamento.
title: Implementare un ritorno a capo rapido dell’annuncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 2%

---


# Implementa un ritorno anticipato dell&#39;interruzione pubblicitaria {#implement-an-early-ad-break-return}

Per l&#39;inserimento di annunci in streaming live, potrebbe essere necessario uscire da un&#39;interruzione pubblicitaria prima che tutti gli annunci nell&#39;interruzione siano riprodotti al completamento.

Ad esempio, la durata dell’interruzione pubblicitaria in alcuni eventi sportivi potrebbe non essere nota prima dell’inizio dell’interruzione. TVSDK fornisce una durata predefinita, ma se il gioco riprende prima del termine dell’interruzione, l’interruzione pubblicitaria deve essere chiusa. Un altro esempio è un segnale di emergenza durante una pausa pubblicitaria in un flusso live.

1. Iscriviti ai marcatori di annunci in uscita/in di copia ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` e `#EXT-X-CUE`).

   Per ulteriori informazioni su come applicare marcatori di annunci in uscita/in, consulta [Generatori di opportunità e risolutori di contenuti](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md).
1. Utilizza un `ContentFactory` personalizzato.
1. In `retrieveGenerators()`, utilizza `SpliceInPlacementOpportunityGenerator`.

   Ad esempio:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Per ulteriori informazioni sull&#39;utilizzo di un `ContentFactory` personalizzato, consulta il passaggio 1 in [Implementare un rilevatore di opportunità personalizzato](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) .

1. Sullo stesso `ContentFactory` personalizzato, implementa `retrieveResolvers` e includi `AuditudeResolver` e `SpliceInCustomResolver`.

   Ad esempio:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

