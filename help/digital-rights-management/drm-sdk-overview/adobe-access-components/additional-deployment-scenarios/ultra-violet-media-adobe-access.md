---
title: Supporti UltraViolet e Adobe Primetime DRM
description: Supporti UltraViolet e Adobe Primetime DRM
copied-description: true
exl-id: 03b01a29-e8e0-4fb5-a685-63a745a6417c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Supporti UltraViolet e Adobe Primetime DRM {#ultraviolet-media-and-adobe-primetime-drm}

Adobe Primetime DRM può essere utilizzato con altre soluzioni di streaming di contenuti di terze parti per configurare un ecosistema di distribuzione dei contenuti multimediali basato su DRM completo e sicuro.

UltraViolet ( [https://www.myuv.com/](https://www.uvvu.com/)) è un sistema di autenticazione dei diritti digitali e di distribuzione basato su cloud che consente ai consumatori di contenuti di intrattenimento digitale domestico di eseguire lo streaming e il download dei contenuti acquistati tramite più piattaforme e dispositivi. Il contenuto UltraViolet verrà scaricato (o inviato in streaming) in un Common File Format (CFF) utilizzando Common Encryption (CENC).

È facile configurare un sistema UltraViolet insieme a Adobe Primetime DRM. Il seguente caso d’uso illustra il comportamento del flusso di contenuto:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. Il proprietario del contenuto codifica e crea pacchetti per il contenuto in CFF. Il pacchetto viene concesso in licenza a un rivenditore per la distribuzione.
1. Il rivenditore carica il contenuto su un provider di servizi digitali, come CDN. Il contenuto è ora disponibile per il download. Tieni presente che alcuni di questi ruoli possono essere svolti da una o più aziende.

   L’utente finale dispone di un dispositivo che supporta Adobe AIR. Inoltre, è necessario installare un&#39;applicazione compatibile con UltraViolet. L&#39;applicazione include il codice necessario per analizzare il CFF e presentarlo per l&#39;utilizzo da parte del runtime. Tutte le operazioni di crittografia sensibili vengono gestite nel runtime protetto.
1. L&#39;applicazione può attivare un&#39;aggiunta al dominio per il dispositivo, che interagisce con il coordinatore. Il coordinatore gestisce un archivio diritti, un database utenti e i domini. Il gestore del dominio del coordinatore viene creato utilizzando l’SDK di Primetime DRM per implementare le operazioni di aggiunta/uscita dal dominio specifiche per Primetime DRM.
1. L’utente può quindi utilizzare l’applicazione per selezionare un video che desidera acquisire dal rivenditore. In genere, il rivenditore fornisce un portale web e gestisce tutte le regole di business.
1. Il rivenditore interagisce quindi con il coordinatore per aggiungere un token di diritti. Il rivenditore reindirizza quindi la richiesta al provider di servizi per il download del contenuto effettivo.
1. Se il dispositivo non dispone ancora di una licenza per il contenuto, attiva una richiesta di licenza utilizzando il CFF. La richiesta include in genere un certificato di dominio, credenziali utente e informazioni sull’applicazione. Il provider di servizi gestisce un server di licenze DRM Primetime (sviluppato utilizzando Primetime DRM SDK) che segue le specifiche UltraViolet.
1. La logica di business UltraViolet del provider di servizi interagisce con il coordinatore in base alle esigenze per recuperare il token di diritti appropriato per determinare se è necessario rilasciare una licenza per contenuti.

   La licenza per contenuti è associata al dominio. L&#39;applicazione client può inserire la licenza nel file CFF. Ora è possibile riprodurre il contenuto nell’applicazione, con tutte le regole di protezione e utilizzo gestite dal componente DRM di Primetime in fase di esecuzione.
1. Altri dispositivi e applicazioni di proprietà dello stesso utente finale possono essere registrati presso il coordinatore. Il contenuto può ora essere caricato su altri dispositivi DRM di Primetime senza richiedere alcuna transazione esterna.
