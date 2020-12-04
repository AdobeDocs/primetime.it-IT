---
seo-title: Informazioni sui certificati
title: Informazioni sui certificati
uuid: 0b7818b4-bd6a-4f2e-94c2-565e0d735bf8
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Informazioni sui certificati {#about-certificates}

L’SDK Adobe Primetime DRM  è disponibile nelle seguenti configurazioni:

* Primetime DRM Production SDK
* SDK valutazione DRM di Primetime
* SDK di prova DRM Primetime

Per utilizzare l&#39;SDK DRM di Primetime per creare un server di licenze, è necessario ottenere certificati digitali da  Adobe. I certificati digitali (denominati anche semplicemente certificati) associano un&#39;entità, ad esempio un singolo, un&#39;organizzazione o un sistema, a una coppia di chiavi pubblica e privata specifica. I certificati digitali possono essere considerati come credenziali elettroniche per la verifica dell&#39;identità di un singolo, sistema o organizzazione.

Per consentire la massima flessibilità e una maggiore sicurezza nelle opzioni di distribuzione, Primetime DRM SDK richiede quattro certificati:

* Certificato del server licenze

   L’SDK utilizza questo certificato per firmare le licenze di contenuto rilasciate ai client.
* Certificato Packager

   L’SDK utilizza questo certificato per generare metadati DRM durante la creazione di pacchetti di contenuto (cifratura).
* Certificato di trasporto

   L’SDK utilizza questo certificato per proteggere la comunicazione tra i client e il server delle licenze.
* Certificato CA di dominio

   I clienti che desiderano implementare un server di dominio necessitano del certificato Domain CA. A differenza degli altri certificati, il certificato Domain CA non è emesso dal Adobe .

>[!NOTE]
>
>Per l’SDK di valutazione e l’SDK di prova, i certificati License Server, Packager e Transport sono combinati in un unico certificato.

