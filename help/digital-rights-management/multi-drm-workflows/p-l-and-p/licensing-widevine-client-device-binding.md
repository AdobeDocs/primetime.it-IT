---
description: In alcuni casi, potete impedire agli utenti finali di riprodurre contenuto su più dispositivi quando il contenuto viene acquistato o affittato. Se il cliente utilizza Expressplay, questo può essere fatto utilizzando le API di Expressplay per associare il token di Expressplay dell'utente al computer dell'utente.
seo-description: In alcuni casi, potete impedire agli utenti finali di riprodurre contenuto su più dispositivi quando il contenuto viene acquistato o affittato. Se il cliente utilizza Expressplay, questo può essere fatto utilizzando le API di Expressplay per associare il token di Expressplay dell'utente al computer dell'utente.
seo-title: Associazione dispositivo
title: Associazione dispositivo
uuid: 351fa33c-4226-4ed5-829c-56b563166fec
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Associazione dispositivo{#device-binding}

In alcuni casi, potete impedire agli utenti finali di riprodurre contenuto su più dispositivi quando il contenuto viene acquistato o affittato. Se il cliente utilizza Expressplay, questo può essere fatto utilizzando le API di Expressplay per associare il token di Expressplay dell&#39;utente al computer dell&#39;utente.

Potete utilizzare le API nel modo seguente.

1. Generare un cookie.
1. Invia una richiesta di generazione token fittizia con il cookie generato associato come una stringa di query (cookie=`<cookie>`) o come intestazioni.
1. Far sì che il computer dell&#39;utente invii una richiesta di licenza al server licenze Expressplay utilizzando il token indicato sopra, ad esempio riproducendo un contenuto fittizio.

   Questa richiesta di licenza fittizia, in caso di esito positivo, associa il device_id dell&#39;utente (calcolato o generato dall&#39;implementazione DRM sul dispositivo dell&#39;utente) al cookie nel back-end di Expressplay. Questo cookie viene quindi utilizzato nel modo seguente:

   * Al momento dell&#39;acquisto/affitto del contenuto, il codice invia una query al back-end di Expressplay per device_id dell&#39;utente inviando il cookie associato ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Inviate una richiesta di generazione di token con la chiave (CEK), l&#39;ID chiave (CEKSID), i criteri e altre informazioni del contenuto acquistato, allegando rispettivamente il cookie e il device_id come parametro di `cookie` correlazione e parametro di restrizione `deviceid` token.

   * Fornite questo token all&#39;utente.

      Questo processo genera un token per il contenuto associato al device_id dell&#39;utente. Quando il computer dell&#39;utente invia una richiesta di licenza con questo token, il back-end Expressplay verifica l&#39;ID dispositivo_id del token con l&#39;ID dispositivo_id della richiesta di licenza.

      Un server di adesione Expressplay di esempio implementa questo flusso di lavoro.
