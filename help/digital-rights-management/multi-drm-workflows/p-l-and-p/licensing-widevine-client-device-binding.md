---
description: In alcuni casi può essere utile impedire agli utenti finali di riprodurre contenuti su più dispositivi quando il contenuto viene acquistato o noleggiato. Se il cliente utilizza Expressplay, è possibile utilizzare le API Expressplay per associare il token Expressplay dell’utente al computer dell’utente.
title: Binding dispositivo
exl-id: 96ead794-e3eb-4059-91d3-a2c351a17ea3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Binding dispositivo{#device-binding}

In alcuni casi può essere utile impedire agli utenti finali di riprodurre contenuti su più dispositivi quando il contenuto viene acquistato o noleggiato. Se il cliente utilizza Expressplay, è possibile utilizzare le API Expressplay per associare il token Expressplay dell’utente al computer dell’utente.

Puoi utilizzare le API nel modo seguente.

1. Genera un cookie.
1. Invia una richiesta di generazione di token fittizi allegando il cookie generato come stringa di query (cookie=`<cookie>`) o come intestazioni.
1. Chiedi al computer dell’utente di inviare una richiesta di licenza al server licenze Expressplay utilizzando il token precedente, ad esempio riproducendo un contenuto fittizio.

   In caso di esito positivo, questa richiesta di licenza fittizia associa il device_id dell’utente (calcolato o generato dall’implementazione DRM sul dispositivo dell’utente) al cookie nel back-end di Expressplay. Questo cookie viene quindi utilizzato nel modo seguente:

   * Al momento dell’acquisto o dell’affitto del contenuto, il codice interroga il back-end Expressplay per il device_id dell’utente inviando il cookie associato ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Invia una richiesta di generazione del token con la chiave del contenuto acquistato (CEK), l’ID chiave (CEKSID), i criteri e altre informazioni, allegando il cookie e il valore device_id rispettivamente come `cookie` parametro di correlazione e `deviceid` parametro di restrizione del token.

   * Fornisci questo token all’utente.

      Questo processo genera un token per il contenuto associato al device_id dell’utente. Quando il computer dell’utente invia una richiesta di licenza con questo token, il back-end di Expressplay controllerà il device_id del token con il device_id della richiesta di licenza.

      Un esempio di Expressplay server di adesione implementa questo flusso di lavoro.
