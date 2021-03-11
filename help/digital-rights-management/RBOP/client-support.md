---
description: Questa sezione descrive le funzioni disponibili con diverse versioni di Flash Player e TVSDK.
title: Supporto client RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Supporto client RBOP {#rbop-client-support}

Questa sezione descrive le funzioni disponibili con diverse versioni di Flash Player e TVSDK.

**Invio di errori** : le piattaforme TVSDK elencate di seguito inviano un errore DRM Runtime quando la risoluzione del contenuto in fase di riproduzione supera la risoluzione consentita per la configurazione del dispositivo definita nel criterio DRM:

* Versioni da 18 a 20 del Flash Player
* Android - Versioni
* iOS - Versioni

>[!NOTE]
>
>* Tutte le piattaforme mobili e di Flash supportano l&#39;invio di errori, tuttavia solo i client TVSDK elencati sopra elaborano errori relativi all&#39;RBOP.
>* Errori client relativi a RBOP [DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371**  - Risoluzione non corretta basata sui vincoli di protezione dell&#39;output contenuti nella licenza.
   >    * **3372**  - La risoluzione del contenuto è maggiore della risoluzione massima specificata nel vincolo di protezione dell&#39;output. (Questo può accadere se qualcuno ha provato a inserire contenuto destinato a un altro dispositivo.)
   >    * **3373**  - La risoluzione del contenuto è maggiore della risoluzione specificata dal vincolo di protezione dell&#39;output attualmente attivo. (Questo significa che dovremo effettuare il downgrade).

>



**Downscaling automatico** : la tecnica utilizzata per eseguire il downscale varia in base alla versione della piattaforma e del Flash Player:

* Versione 21 del Flash Player: Supporta RBOP con downscaling automatico (commutazione a bit rate intelligente)
* Firefox versione 38 e successive su Windows (con Access CDM): L&#39;Adobe scarica automaticamente un flusso di bit rate più alto a uno più basso (invece di scaricare un flusso di livello inferiore).

>[!NOTE]
>
>Queste piattaforme ridimensionano automaticamente il video e visualizzano il contenuto a una risoluzione inferiore o uguale a quella specificata dal criterio DRM. Con questa funzione, il contenuto verrà sempre riprodotto sul client, purché sia presente un flusso disponibile che soddisfa le restrizioni dei criteri DRM.

**Protezione**  output legacy: i client che utilizzano Flash Player precedenti alla versione 18 possono gestire solo restrizioni OP legacy. I clienti con versione 18 o successiva del Flash Player possono gestire le restrizioni legacy o RBOP. Se si impostano le restrizioni RBOP, è inoltre necessario impostare le restrizioni OP legacy per i client meno recenti. Per i client che supportano RBOP, le restrizioni RBOP superano le restrizioni OP legacy.
