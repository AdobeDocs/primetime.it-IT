---
description: Questa sezione descrive le funzioni disponibili con diverse versioni di Flash Player e TVSDK.
title: Supporto client RBOP
exl-id: 1120587e-45cf-45cc-8b41-1886ab2ed2a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Supporto client RBOP {#rbop-client-support}

Questa sezione descrive le funzioni disponibili con diverse versioni di Flash Player e TVSDK.

**Invio errori** - Le piattaforme TVSDK elencate di seguito inviano un errore di runtime DRM quando la risoluzione del contenuto riprodotto supera la risoluzione consentita per la configurazione del dispositivo definita nella policy DRM:

* Versioni Flash Player da 18 a 20
* Android - Versioni
* iOS - Versioni

>[!NOTE]
>
>* Tutte le piattaforme di Flash e mobili supportano Error Dispatch, tuttavia solo i client TVSDK elencati sopra elaborano gli errori relativi alla RBOP.
>* Relativo a RBOP [Errori client DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371** - Risoluzione in formato non valido in base ai vincoli di protezione dell&#39;output nella licenza.
   >    * **3372** - La risoluzione del contenuto è maggiore della risoluzione massima specificata nel vincolo di protezione dell&#39;output. (Questo può verificarsi se qualcuno ha tentato di inserire contenuto destinato a un altro dispositivo).
   >    * **3373** - La risoluzione del contenuto è maggiore della risoluzione specificata dal vincolo di protezione dell&#39;output attualmente attivo. (Questo significa che dovremo effettuare il downgrade).
>


**Downscaling automatico** - La tecnica utilizzata per effettuare il downscale varia in base alla piattaforma e alla versione del Flash Player:

* Flash Player versione 21: supporta RBOP con downscaling automatico (commutazione bitrate intelligente)
* Firefox versione 38 e successive su Windows (con Access CDM): Adobe esegue automaticamente il downgrade di un flusso con bitrate superiore a uno inferiore (anziché scaricare un flusso con livello inferiore).

>[!NOTE]
>
>Queste piattaforme eseguono automaticamente il downscale dei video e visualizzano il contenuto con una risoluzione inferiore o uguale a quella specificata dalla policy DRM. Con questa funzione, il contenuto viene sempre riprodotto sul client, purché sia disponibile un flusso che rispetti le restrizioni della policy DRM.

**Protezione dell&#39;output legacy** - I clienti che utilizzano Flash Player precedenti alla versione 18 possono gestire solo le restrizioni OP legacy. I client con versione di Flash Player 18 e successive possono gestire le restrizioni legacy o RBOP. Se si impostano restrizioni RBOP, è necessario impostare anche restrizioni OP legacy per i client meno recenti. Per i client che supportano la RBOP, le restrizioni RBOP superano le restrizioni OP legacy.
