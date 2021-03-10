---
description: Il server di riferimento SEES mostra come abilitare il servizio di adesione per il binding dei dispositivi utilizzando ExpressPlay.
title: Autorizzazione di associazione a dispositivi del servizio di riferimento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Servizio di riferimento: Autorizzazione a associazione di dispositivi {#reference-service-device-binding-entitlement}

Il server di riferimento SEES mostra come abilitare il servizio di adesione per il binding dei dispositivi utilizzando ExpressPlay.

>[!NOTE]
>
>Il servizio di adesione associato al dispositivo può anche essere limitato nel tempo o fornire una durata di noleggio.

Per avviare le informazioni `device_id`, riproduci un contenuto fittizio M3U8. È quindi possibile incorporare un cookie nel token ExpressPlay, generare un SPC (che contiene `device_id`) e inviare un `getToken` al server ExpressPlay.

![](assets/fees-device-binding.png)

La sequenza inizia riproducendo un fittizio M3U8. Viene inviato un cookie al server SEES per ottenere l’URL del token ExpressPlay. Dopo aver ricevuto l&#39;URL del token ExpressPlay associato a cookie, il passaggio successivo consiste nel generare l&#39;SPC e inviarlo al server ExpressPlay. Il server ExpressPlay estrae il `device_id` da SPC, il cookie dall&#39;URL del token ExpressPlay, e inserisce il cookie e `device_id` nel registro delle transazioni.

Il cliente effettua una richiesta di licenza reale a SEES inviando lo stesso cookie. SEES utilizza il cookie per recuperare il `device_id` dal server ExpressPlay.

SEES richiede un token ExpressPlay associato al dispositivo e al tempo e restituisce tale token al client.

Il cliente effettua la richiesta di licenza con il token ExpressPlay.

Il server ExpressPlay confronta il `device_id` nell’SPC con il `device_id` nel token ExpressPlay. Il server ExpressPlay rilascia una licenza solo se i due valori `device_id` corrispondono.
