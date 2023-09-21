---
title: Informazioni sui certificati
description: Informazioni sui certificati
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Informazioni sui certificati {#about-certificates}

L’SDK di Adobe Primetime DRM è disponibile nelle seguenti configurazioni:

* SDK di produzione DRM di Primetime
* SDK di valutazione DRM di Primetime
* SDK di prova di Primetime DRM

Per utilizzare Primetime DRM SDK per creare un server licenze, è necessario ottenere certificati digitali da Adobe. I certificati digitali (detti anche certificati) associano un&#39;entità, ad esempio un individuo, un&#39;organizzazione o un sistema, a una specifica coppia di chiavi pubblica e privata. I certificati digitali possono essere considerati credenziali elettroniche che verificano l’identità di un individuo, un sistema o un’organizzazione.

Per consentire la massima flessibilità e una maggiore sicurezza nelle opzioni di distribuzione, l’SDK della DRM di Primetime richiede quattro certificati:

* Certificato server licenze

  L’SDK utilizza questo certificato per firmare le licenze per contenuti rilasciate ai client.
* Certificato Packager

  L’SDK utilizza questo certificato per generare metadati DRM durante la creazione del pacchetto (crittografia) del contenuto.
* Certificato di trasporto

  L’SDK utilizza questo certificato per proteggere la comunicazione tra i client e il server licenze.
* Certificato CA di dominio

  I clienti che desiderano implementare un server di dominio devono disporre del certificato CA di dominio. A differenza degli altri certificati, il certificato CA del dominio non viene emesso da Adobe.

>[!NOTE]
>
>Per l’SDK di valutazione e l’SDK di prova, i certificati Server licenze, Packager e Trasporto sono combinati in un unico certificato.
