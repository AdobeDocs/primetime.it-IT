---
description: Il server di riferimento SEES mostra come abilitare il servizio di adesione per l'associazione dei dispositivi tramite ExpressPlay.
title: Autorizzazione associazione dispositivo servizio di riferimento
exl-id: 91f9d406-f3f9-47d3-aa50-f47c4e81b9fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Servizio di riferimento: diritto di associazione dispositivo {#reference-service-device-binding-entitlement}

Il server di riferimento SEES mostra come abilitare il servizio di adesione per l&#39;associazione dei dispositivi tramite ExpressPlay.

>[!NOTE]
>
>Il servizio di adesione per dispositivi mobili può anche essere vincolato al tempo o fornire una durata di noleggio.

Per avviare `device_id` informazioni, riproduzione di un contenuto M3U8 fittizio. Puoi quindi incorporare un cookie nel token ExpressPlay, generare un SPC (contenente `device_id`) e invia un `getToken` su ExpressPlay Server.

![](assets/fees-device-binding.png)

La sequenza inizia con la riproduzione di un M3U8 fittizio. Viene inviato un cookie al server SEES per ottenere l’URL del token ExpressPlay. Dopo aver ricevuto l&#39;URL del token ExpressPlay associato ai cookie, il passaggio successivo consiste nel generare l&#39;SPC e inviarlo al server ExpressPlay. Il server ExpressPlay estrae `device_id` da SPC, il cookie dall’URL del token ExpressPlay e inserisce il cookie e `device_id` nel registro delle transazioni.

Il client invia una vera richiesta di licenza a SEES inviando lo stesso cookie. SEES utilizza il cookie per recuperare il `device_id` dal server ExpressPlay.

SEES richiede un token ExpressPlay associato a un dispositivo e a un orario e restituisce tale token al client.

Il client effettua la richiesta di licenza con il token ExpressPlay.

Il server ExpressPlay confronta `device_id` nel riassunto delle caratteristiche del prodotto con `device_id` nel token ExpressPlay. Il server ExpressPlay rilascia una licenza solo se i due `device_id` i valori corrispondono.
