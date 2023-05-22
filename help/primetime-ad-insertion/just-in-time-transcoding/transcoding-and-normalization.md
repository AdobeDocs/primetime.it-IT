---
title: Transcodifica e normalizzazione
description: Transcodifica e normalizzazione
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
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
