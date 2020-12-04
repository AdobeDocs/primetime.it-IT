---
description: Questa sezione descrive le funzioni disponibili con diverse versioni di Flash Player e TVSDK.
seo-description: Questa sezione descrive le funzioni disponibili con diverse versioni di Flash Player e TVSDK.
seo-title: Supporto client RBOP
title: Supporto client RBOP
uuid: d1d0f788-7bc1-488c-807e-be47f83725e9
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# Supporto client RBOP {#rbop-client-support}

Questa sezione descrive le funzioni disponibili con diverse versioni di Flash Player e TVSDK.

**Errore**  - Le piattaforme TVSDK elencate di seguito inviano un errore DRM Runtime quando la risoluzione del contenuto in corso di riproduzione supera la risoluzione consentita per la configurazione del dispositivo definita nel criterio DRM:

* Versioni Flash Player da 18 a 20
* Android - Versioni
* iOS - Versioni

>[!NOTE]
>
>* Tutte le piattaforme mobili e di Flash supportano la trasmissione degli errori, ma solo i client TVSDK elencati sopra elaborano gli errori relativi alla RBOP.
>* Errori client DRM [correlati a RBOP](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371** - Risoluzione non corretta basata sui limiti di protezione dell&#39;output contenuti nella licenza.
   >    * **3372**  - La risoluzione del contenuto è maggiore della risoluzione massima specificata nel vincolo di protezione dell&#39;output. (Questo può verificarsi se qualcuno ha provato a inserire contenuto destinato a un altro dispositivo).
   >    * **3373**  - La risoluzione del contenuto è superiore a quella specificata dal vincolo di protezione dell&#39;output attualmente attivo. (Questo significa che dovremo eseguire il downgrade).

>



**Download**  automatico - La tecnica utilizzata per eseguire il downscale varia in base alla piattaforma e alla versione del Flash Player:

* Versione Flash Player 21: Supporta RBOP con downscaling automatico (commutazione bitrate intelligente)
* Firefox versione 38 e successive su Windows (con Access CDM):  Adobe esegue automaticamente il downgrade di un flusso bitrate superiore a uno inferiore (invece di scaricare un flusso di livello inferiore).

>[!NOTE]
>
>Queste piattaforme impostano automaticamente il video in scala ridotta e visualizzano il contenuto a una risoluzione inferiore o uguale a quella specificata dal criterio DRM. Grazie a questa funzione, il contenuto verrà sempre riprodotto al client, purché sia disponibile un flusso che soddisfi le restrizioni dei criteri DRM.

**Protezione**  output legacy: i client che utilizzano Flash Player precedenti alla versione 18 possono gestire solo le limitazioni OP legacy. I client con versione di Flash Player 18 e versioni successive possono gestire le limitazioni legacy o RBOP. Se si impostano le restrizioni di RBOP, è inoltre necessario impostare le restrizioni di OP legacy per i client meno recenti. Per i client che supportano RBOP, le restrizioni RBOP superano le restrizioni OP legacy.
