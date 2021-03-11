---
title: Informazioni sui certificati
description: Informazioni sui certificati
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Informazioni sui certificati {#about-certificates}

L’SDK DRM di Adobe Primetime è disponibile nelle seguenti configurazioni:

* SDK per produzione DRM di Primetime
* SDK di valutazione DRM di Primetime
* SDK di prova DRM di Primetime

Per utilizzare l&#39;SDK DRM di Primetime per creare un server di licenze, è necessario ottenere certificati digitali da Adobe. I certificati digitali (denominati anche semplicemente certificati) associano un’entità, ad esempio una singola, organizzazione o sistema, a una coppia di chiavi pubblica e privata specifica. I certificati digitali possono essere considerati credenziali elettroniche che verificano l&#39;identità di una persona, di un sistema o di un&#39;organizzazione.

Per consentire la massima flessibilità e una maggiore sicurezza nelle opzioni di distribuzione, Primetime DRM SDK richiede quattro certificati:

* Certificato del server licenze

   L’SDK utilizza questo certificato per firmare le licenze di contenuto rilasciate ai client.
* Certificato del pacchetto

   L’SDK utilizza questo certificato per generare metadati DRM durante la creazione del pacchetto (crittografia) del contenuto.
* Certificato di trasporto

   L’SDK utilizza questo certificato per proteggere la comunicazione tra i client e il server licenze.
* Certificato CA del dominio

   I clienti che desiderano implementare un server di dominio devono disporre del certificato Domain CA. A differenza degli altri certificati, il certificato Domain CA non viene rilasciato dall’Adobe.

>[!NOTE]
>
>Per l’SDK di valutazione e l’SDK di prova, i certificati License Server, Packager e Transport sono combinati in un unico certificato.

