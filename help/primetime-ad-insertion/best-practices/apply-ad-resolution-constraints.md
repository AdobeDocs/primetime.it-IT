---
title: Applicare vincoli di risoluzione annuncio
description: Applicare vincoli di risoluzione annuncio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Applicare vincoli di risoluzione annuncio {#apply-ad-resolution-constraints}

In alcuni casi, determinati provider di annunci sono lenti nel rispondere e questo può causare un aumento dei tempi di avvio dei video. Primetime Ad Insertion supporta i timeout delle richieste degli annunci e l’intera fase di risoluzione degli annunci per limitare l’impatto di questi provider di annunci lenti.  Gli annunci di fallback possono essere inseriti anche se i provider di annunci a valle sono troppo lenti per rispondere.  Per ulteriori informazioni, consulta [`ptadtimeout` Parametro nell’API Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
