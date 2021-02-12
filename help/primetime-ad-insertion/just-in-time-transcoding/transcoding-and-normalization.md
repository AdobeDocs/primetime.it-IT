---
title: Transcodifica e normalizzazione
description: null
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Transcodifica e normalizzazione {#transcoding-and-normalization}

Primetime  Ad Insertion tenterà di garantire un&#39;esperienza di visualizzazione coerente tra i contenuti e gli annunci, cercando di trovare una corrispondenza:

1. Codec flusso sorgente e bitrate, selezionando sempre la massima qualità/bitrate creativa durante la transcodifica

1. Dimensioni dei frammenti del flusso di origine (HLS/#EXT-X-TARGETDURATION)

1. Formati creativi preferiti per la transcodifica

1. Livellamento automatico dell&#39;audio per garantire un livello dB coerente tra tutte le creatività degli annunci.

>[!NOTE]
>
>Le risorse HLS generate dalla transcodifica del tempo di  Primetime producono risorse HLS della versione 3, indipendentemente dalla versione HLS definita nel contenuto.