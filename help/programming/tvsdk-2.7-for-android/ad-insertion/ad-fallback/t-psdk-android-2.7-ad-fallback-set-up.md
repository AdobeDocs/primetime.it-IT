---
description: È possibile abilitare il fallback quando un annuncio VMAP in linea contiene un tipo di supporto non valido.
title: Definire il comportamento di fallback ad per gli annunci in linea VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Definire il comportamento di fallback ad per gli annunci in linea VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

È possibile abilitare il fallback quando un annuncio VMAP in linea contiene un tipo di supporto non valido.

1. Impostare `setFallbackOnInvalidCreativeEnabled` su `true` per far sì che VMAP torni quando il tipo di supporto per un annuncio lineare/in linea non è valido per HLS.

   Il valore predefinito è `false`. Se un annuncio lineare non riesce perché ha un tipo di supporto non valido o perché non può essere ricompilato, questo flag consente a Primetime ad DECISIONING di seguire lo stesso comportamento di fallback come se l&#39;annuncio fosse un wrapper VAST vuoto.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

