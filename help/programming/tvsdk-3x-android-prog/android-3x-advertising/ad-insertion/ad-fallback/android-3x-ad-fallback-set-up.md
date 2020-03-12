---
description: È possibile abilitare il fallback quando un elemento multimediale VMAP in linea contiene un tipo di supporto non valido.
seo-description: È possibile abilitare il fallback quando un elemento multimediale VMAP in linea contiene un tipo di supporto non valido.
seo-title: Definizione del comportamento fallback ad annunci in linea VMAP
title: Definizione del comportamento fallback ad annunci in linea VMAP
uuid: bc8cb0b4-5ea9-429b-ab5d-746c6f03e74b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Definizione del comportamento fallback ad annunci in linea VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

È possibile abilitare il fallback quando un elemento multimediale VMAP in linea contiene un tipo di supporto non valido.

1. Impostato `setFallbackOnInvalidCreativeEnabled` per `true` avere VMAP fall back quando il tipo di supporto per un annuncio lineare/inline non è valido per HLS.

   Il valore predefinito è `false`. Se un annuncio lineare ha un tipo di supporto non valido o non può essere reinserito in un pacchetto, questo flag consente a Primetime ad DECISION di seguire lo stesso comportamento di fallback come se l&#39;annuncio fosse un wrapper VAST vuoto.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
