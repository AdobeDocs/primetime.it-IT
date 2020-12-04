---
description: In alcuni casi, il contenuto non può essere riprodotto. Qualsiasi numero di situazioni può causare questo problema, inclusi errori nello stack di rete del browser, livello di trasporto, sistema operativo, runtime di Flash Player o sistema DRM di Primetime.
seo-description: In alcuni casi, il contenuto non può essere riprodotto. Qualsiasi numero di situazioni può causare questo problema, inclusi errori nello stack di rete del browser, livello di trasporto, sistema operativo, runtime di Flash Player o sistema DRM di Primetime.
seo-title: Panoramica sugli errori di verifica
title: Panoramica sugli errori di verifica
uuid: 44b4ab0e-5f08-44b0-bcb5-a869f6add69b
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# Errori di verifica {#triaging-errors}

In alcuni casi, il contenuto non può essere riprodotto. Qualsiasi numero di situazioni può causare questo problema, inclusi errori nello stack di rete del browser, livello di trasporto, sistema operativo, runtime di Flash Player o sistema DRM di Primetime.

Il primo passaggio diagnostico consiste nel determinare se il problema si manifesta senza la crittografia DRM introdotta nell&#39;equazione. Tentate di creare un pacchetto per il contenuto, ma chiedete al packager di non cifrare il contenuto. Se il problema persiste, è probabile che si tratti di un problema di codifica o di creazione di pacchetti di contenuto o di un punto qualsiasi dell&#39;infrastruttura di rete. Se il problema si risolve quando il contenuto viene incluso in un pacchetto senza crittografia, l&#39;errore di riproduzione è probabilmente dovuto a un problema DRM ed è necessario avviare una verifica client/server.

Primetime DRM (al di fuori di Primetime Cloud DRM) è sul mercato da diversi anni. Di conseguenza, è disponibile una vasta gamma di informazioni fornite dalla community per la risoluzione dei problemi e la configurazione di DRM di Primetime.  Adobe ha fornito un forum per gli utenti DRM di Primetime (precedentemente denominato  accesso al Adobe) per aggregare e condividere problemi e risoluzioni. Per determinare se il problema è già stato discusso, controllate: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Prova errori client {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Se il contenuto non viene riprodotto, esaminate il pannello a destra dei lettori video di esempio, che registrerà eventuali `DRMErrorEvent` che si verificano. Se si verifica un evento di errore, verrà correlata a uno degli errori di runtime di Flash Player:

* [Riferimento](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages) messaggio di errore client DRM; o
* [AS3 Flash Errori](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html)  runtime (i problemi DRM iniziano alla 3300)

