---
description: Talvolta può accadere che il contenuto non possa essere riprodotto. Ciò può essere causato da qualsiasi numero di situazioni, inclusi errori nello stack di rete del browser, nel livello di trasporto, nel sistema operativo, nel runtime di Flash Player o nel sistema DRM Primetime.
title: Panoramica sugli errori di verifica
exl-id: fe94d0a4-4f3c-4b0e-b830-a7a83bac1e85
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Errori di valutazione {#triaging-errors}

Talvolta può accadere che il contenuto non possa essere riprodotto. Ciò può essere causato da qualsiasi numero di situazioni, inclusi errori nello stack di rete del browser, nel livello di trasporto, nel sistema operativo, nel runtime di Flash Player o nel sistema DRM Primetime.

Il primo passaggio diagnostico consiste nel determinare se il problema si manifesta senza la crittografia DRM introdotta nell&#39;equazione. Tenta di creare un pacchetto del contenuto, ma ordina al packager di non crittografarlo. Se il problema persiste, è probabile che si tratti di un problema di codifica o creazione di pacchetti del contenuto o di un percorso all&#39;interno dell&#39;infrastruttura di rete. Se il problema scompare quando il contenuto viene collocato senza crittografia, è probabile che la riproduzione non riesca a causa di un problema DRM e si consiglia di effettuare una prova client/server.

Primetime DRM (al di fuori di Primetime Cloud DRM) è presente sul mercato da diversi anni. Di conseguenza, esistono numerose informazioni di origine comunitaria sulla risoluzione dei problemi e la configurazione di Primetime DRM. Adobe ha fornito un forum per gli utenti di Primetime DRM (precedentemente denominato Accesso agli Adobi) per aggregare e condividere problemi e risoluzioni. Per determinare se il problema è stato discusso in precedenza, controlla: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Tentativo di errori client {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Se il contenuto non viene riprodotto, esamina il pannello a destra dei lettori video di esempio, in cui verranno registrate le `DRMErrorEvent` che si verifica. Se si verifica un evento di errore, verrà correlato a uno degli errori di runtime del Flash Player:

* [Riferimento messaggio di errore client DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages); o
* [Errori di runtime del Flash AS3](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (problemi DRM iniziano a 3300)
