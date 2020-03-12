---
description: Il server di riferimento SEES mostra come abilitare il servizio di adesione per il binding dei dispositivi utilizzando ExpressPlay.
seo-description: Il server di riferimento SEES mostra come abilitare il servizio di adesione per il binding dei dispositivi utilizzando ExpressPlay.
seo-title: Servizio di riferimento Adesione a un dispositivo
title: Servizio di riferimento Adesione a un dispositivo
uuid: 22ce2f8e-1758-4528-8caf-60d209839afe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Servizio di riferimento: Adesione a binding dispositivo {#reference-service-device-binding-entitlement}

Il server di riferimento SEES mostra come abilitare il servizio di adesione per il binding dei dispositivi utilizzando ExpressPlay.

>[!NOTE]
>
>Il servizio di adesione associato al dispositivo può anche essere limitato nel tempo o fornire una durata di noleggio.

Per avviare le `device_id` informazioni, riprodurre un contenuto fittizio M3U8. Potete quindi incorporare un cookie nel token ExpressPlay, generare un SPC (che contiene l&#39; `device_id`) e inviare un cookie `getToken` al server ExpressPlay.

![](assets/fees-device-binding.png)

La sequenza inizia riproducendo un fittizio M3U8. Viene inviato un cookie al server SEES per ottenere l’URL del token ExpressPlay. Dopo aver ricevuto l&#39;URL del token ExpressPlay associato a cookie, il passaggio successivo consiste nel generare l&#39;SPC e inviarlo al server ExpressPlay. Il server ExpressPlay estrae il cookie `device_id` da SPC, il cookie dall&#39;URL del token ExpressPlay, e inserisce il cookie e `device_id` nel registro delle transazioni.

Il cliente fa una richiesta di licenza reale a SEES inviando lo stesso cookie. SEES utilizza il cookie per recuperare i dati `device_id` dal server ExpressPlay.

SEES richiede un token ExpressPlay associato sia al dispositivo che al tempo e restituisce tale token al client.

Il cliente effettua la richiesta di licenza con il token ExpressPlay.

Il server ExpressPlay confronta il `device_id` contenuto dell&#39;SPC con quello `device_id` del token ExpressPlay. Il server ExpressPlay rilascia una licenza solo se i due `device_id` valori corrispondono.
