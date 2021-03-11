---
description: In alcuni casi, potresti voler impedire agli utenti finali di riprodurre contenuti su più dispositivi quando il contenuto viene acquistato o affittato. Se il cliente utilizza Expressplay, è possibile eseguire questa operazione utilizzando le API Expressplay per associare il token Expressplay dell’utente al computer dell’utente.
title: Binding dei dispositivi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Binding dei dispositivi{#device-binding}

In alcuni casi, potresti voler impedire agli utenti finali di riprodurre contenuti su più dispositivi quando il contenuto viene acquistato o affittato. Se il cliente utilizza Expressplay, è possibile eseguire questa operazione utilizzando le API Expressplay per associare il token Expressplay dell’utente al computer dell’utente.

Puoi utilizzare le API nel modo seguente.

1. Genera un cookie.
1. Invia una richiesta di generazione del token fittizio con il cookie generato allegato come stringa di query (cookie=`<cookie>`) o come intestazioni.
1. Chiedi al computer dell’utente di inviare una richiesta di licenza al server licenze Expressplay utilizzando il token riportato sopra, ad esempio riproducendo un contenuto fittizio.

   Questa richiesta di licenza fittizia, in caso di esito positivo, associa l’ID dispositivo_id dell’utente (calcolato o generato dall’implementazione DRM sul dispositivo dell’utente) al cookie nel back-end Expressplay. Questo cookie viene quindi utilizzato nel modo seguente:

   * Al momento dell’acquisto o dell’affitto del contenuto, il codice invia una query al back-end Expressplay per il device_id dell’utente inviando il cookie associato ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Invia una richiesta di generazione del token con la chiave del contenuto acquistato (CEK), keyID (CEKSID), i criteri e altre informazioni, allegando il cookie e device_id sopra rispettivamente come il parametro di correlazione `cookie` e il parametro di restrizione del token `deviceid`.

   * Fornisci questo token all’utente.

      Questo processo genera un token per il contenuto associato all’ID_dispositivo dell’utente. Quando il computer dell’utente invia una richiesta di licenza con questo token, il back-end Expressplay controlla il device_id del token con il device_id della richiesta di licenza.

      Un server di adesione Expressplay di esempio implementa questo flusso di lavoro.
