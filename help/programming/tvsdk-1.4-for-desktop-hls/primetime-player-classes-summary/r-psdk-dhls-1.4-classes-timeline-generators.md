---
description: Queste classi sono utili per rilevare le opportunità in una timeline per il posizionamento di contenuti, come gli annunci.
title: Classi dei generatori di timeline
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Classi dei generatori di timeline{#timeline-generators-classes}

Queste classi sono utili per rilevare le opportunità in una timeline per il posizionamento di contenuti, come gli annunci.

Pacchetto [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Nome | Descrizione |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | Classe che crea un&#39;opportunità iniziale per la modalità di segnalazione pubblicitaria specificata. |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Classe base per tutti i generatori di opportunità. |
| [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Interfaccia utilizzata dai generatori di opportunità per comunicare con i componenti TVSDK. |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | Classe che controlla la timeline di riproduzione e rileva le opportunità di posizionamento degli annunci inseriti nel manifesto come commenti SpliceOut. |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Implementazione predefinita di un generatore di opportunità che utilizza informazioni sui metadati temporizzati per rilevare e generare opportunità pubblicitarie. |
