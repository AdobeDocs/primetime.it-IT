---
description: A volte, si verificano casi in cui il contenuto non può essere riprodotto. Qualsiasi numero di situazioni può causare questo, inclusi gli errori nello stack di rete del browser, livello di trasporto, sistema operativo, runtime di Flash Player o sistema DRM Primetime.
title: Panoramica sugli errori di verifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Errori di verifica {#triaging-errors}

A volte, si verificano casi in cui il contenuto non può essere riprodotto. Qualsiasi numero di situazioni può causare questo, inclusi gli errori nello stack di rete del browser, livello di trasporto, sistema operativo, runtime di Flash Player o sistema DRM Primetime.

Il primo passo diagnostico è quello di determinare se il problema si manifesta senza la crittografia DRM introdotta nell&#39;equazione. Tentativo di creare un pacchetto per il contenuto, ma istruzione al gestore di pacchetti di non crittografare il contenuto. Se il problema esiste ancora, è probabile che si tratti di un problema di codifica o creazione di pacchetti del contenuto o di un punto qualsiasi dell&#39;infrastruttura di rete. Se il problema scompare quando il contenuto viene assemblato senza crittografia, l&#39;errore di riproduzione è probabilmente dovuto a un problema DRM e dovresti effettuare una valutazione client/server.

Primetime DRM (al di fuori di Primetime Cloud DRM) è sul mercato da diversi anni. In quanto tale, esistono numerose informazioni provenienti dalla community sulla risoluzione dei problemi e sulla configurazione di DRM di Primetime. Adobe ha fornito un forum per gli utenti DRM di Primetime (precedentemente denominato Adobe Access) per aggregare e condividere problemi e risoluzioni. Per determinare se il problema è già stato discusso, controlla: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Prova degli errori client {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Se il contenuto non viene riprodotto, esaminare il pannello laterale destro dei lettori video di esempio, che registra qualsiasi `DRMErrorEvent` che si verifica. Se si verifica un evento di errore, questa verrà correlata a uno dei Flash Player Errori di runtime :

* [Riferimento](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages) messaggio di errore client DRM; o
* [Errori di runtime di Flash AS3](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html)  (i problemi DRM iniziano a 3300)

