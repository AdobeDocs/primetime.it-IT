---
title: Transcodifica e normalizzazione
description: Transcodifica e normalizzazione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Transcodifica e normalizzazione {#transcoding-and-normalization}

Primetime Ad Insertion tenterà di garantire un’esperienza di visualizzazione coerente tra contenuti e annunci tentando di trovare una corrispondenza con:

1. Codec di streaming sorgente e bitrate, selezionando sempre la qualità/bitrate creativo più elevata durante la transcodifica

1. Dimensioni dei frammenti del flusso di origine (HLS/#EXT-X-TARGETDURATION)

1. Formati creativi preferiti per la transcodifica

1. Livellamento automatico dell&#39;audio per garantire un livello dB coerente su tutte le creatività pubblicitarie.

>[!NOTE]
>
>Le risorse HLS generate dalla transcodifica just-in-time di Primetime Ad Insertion producono risorse HLS della versione 3, indipendentemente dalla versione HLS definita nel contenuto.
