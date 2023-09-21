---
description: È possibile abilitare il fallback quando un annuncio in linea VMAP contiene un tipo di supporto non valido.
title: Definire il comportamento degli annunci di fallback per gli annunci in linea VMAP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Definire il comportamento degli annunci di fallback per gli annunci in linea VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

È possibile abilitare il fallback quando un annuncio in linea VMAP contiene un tipo di supporto non valido.

1. Imposta `setFallbackOnInvalidCreativeEnabled` a `true` per eseguire il fallback di VMAP quando il tipo di supporto per un annuncio lineare/in linea non è valido per HLS.

   Il valore predefinito è `false`. Se un annuncio lineare ha esito negativo perché presenta un tipo di contenuto multimediale non valido o perché l’annuncio non può essere ricompilato, questo flag consente a Primetime ad decisioningdi seguire lo stesso comportamento di fallback come se l’annuncio fosse un wrapper VAST vuoto.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
