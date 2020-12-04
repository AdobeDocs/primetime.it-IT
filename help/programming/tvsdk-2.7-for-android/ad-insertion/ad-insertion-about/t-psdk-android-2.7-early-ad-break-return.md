---
description: Per l'inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un'interruzione di annuncio prima che tutti gli annunci nell'interruzione siano riprodotti al completamento.
seo-description: Per l'inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un'interruzione di annuncio prima che tutti gli annunci nell'interruzione siano riprodotti al completamento.
seo-title: Implementazione di un ritorno a capo rapido
title: Implementazione di un ritorno a capo rapido
uuid: c67f2158-5df4-458c-a27a-6329c5d26638
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---


# Implementazione di un ritorno anticipato all&#39;interruzione dell&#39;annuncio {#implement-an-early-ad-break-return}

Per l&#39;inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un&#39;interruzione di annuncio prima che tutti gli annunci nell&#39;interruzione siano riprodotti al completamento.

Ad esempio, la durata dell&#39;interruzione dell&#39;annuncio in alcuni eventi sportivi potrebbe non essere nota prima dell&#39;inizio dell&#39;interruzione. TVSDK fornisce una durata predefinita, ma se il gioco riprende prima del termine dell&#39;interruzione, è necessario uscire dall&#39;interruzione dell&#39;annuncio. Un altro esempio è rappresentato da un segnale di emergenza durante un&#39;interruzione pubblicitaria in un flusso live.

1. Iscrivetevi a `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` e `#EXT-X-CUE`, che rappresentano la giunzione in uscita/splice nei marcatori.

   Per ulteriori informazioni su come unire marcatori di annunci in uscita/in, consultate [Generatori di opportunità e risolutori di contenuti](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md).

1. Utilizzate un `ContentFactory` personalizzato.
1. In `retrieveGenerators`, utilizzare il simbolo `SpliceInPlacementOpportunityGenerator`.

   Ad esempio:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Per ulteriori informazioni sull&#39;utilizzo di un `ContentFactory` personalizzato, vedere il passaggio 1 in [Implementare un generatore di opportunità personalizzato](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md).

1. Sulla stessa `ContentFactory` personalizzata, implementate `retrieveResolvers` e includete `AuditudeResolver` e `SpliceInCustomResolver`.

   Ad esempio:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

