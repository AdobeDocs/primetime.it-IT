---
description: È possibile abilitare il fallback quando un elemento multimediale VMAP in linea contiene un tipo di supporto non valido.
seo-description: È possibile abilitare il fallback quando un elemento multimediale VMAP in linea contiene un tipo di supporto non valido.
seo-title: Definizione del comportamento fallback ad annunci in linea VMAP
title: Definizione del comportamento fallback ad annunci in linea VMAP
uuid: a7b5c9a6-f546-4d3a-9d49-7e5484acff7a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Definizione del comportamento fallback ad annunci in linea VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

È possibile abilitare il fallback quando un elemento multimediale VMAP in linea contiene un tipo di supporto non valido.

1. Impostate `setFallbackOnInvalidCreativeEnabled` su `true` affinché VMAP venga ripristinato quando il tipo di supporto per un annuncio lineare/inline non è valido per HLS.

   Il valore predefinito è `false`. Se un annuncio lineare ha un tipo di supporto non valido o non può essere reinserito in un pacchetto, questo flag consente a Primetime ad DECISION di seguire lo stesso comportamento di fallback come se l&#39;annuncio fosse un wrapper VAST vuoto.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

