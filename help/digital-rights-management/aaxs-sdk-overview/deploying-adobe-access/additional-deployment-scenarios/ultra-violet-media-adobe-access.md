---
description: L'accesso Adobe può essere utilizzato con altre soluzioni di streaming di contenuti di terze parti per configurare un ecosistema di distribuzione dei contenuti multimediali basato su DRM completo e sicuro.
title: Supporto UltraViolet e accesso agli Adobi
exl-id: cca476a4-1961-46d8-aad4-bc7c996d7b02
source-git-commit: 8d7a4f69a6400b0c3242d4cb0c5daac81f27db3a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Supporto UltraViolet e accesso agli Adobi {#ultraviolet-media-and-adobe-access}

L&#39;accesso Adobe può essere utilizzato con altre soluzioni di streaming di contenuti di terze parti per configurare un ecosistema di distribuzione dei contenuti multimediali basato su DRM completo e sicuro.

UltraViolet è un sistema di autenticazione dei diritti digitali e di distribuzione basato su cloud che consente ai consumatori di contenuti di intrattenimento digitale domestico di eseguire lo streaming e il download dei contenuti acquistati tramite più piattaforme e dispositivi. Il contenuto UltraViolet verrà scaricato (o inviato in streaming) in un Common File Format (CFF) utilizzando Common Encryption (CENC).

È facile impostare un sistema UltraViolet insieme all&#39;accesso Adobe. Il seguente caso d’uso illustra il comportamento del flusso di contenuto:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. Il proprietario del contenuto codifica e crea pacchetti per il contenuto in CFF. Il pacchetto viene concesso in licenza a un rivenditore per la distribuzione.
1. Il rivenditore carica il contenuto su un provider di servizi digitali, come CDN. Il contenuto è ora disponibile per il download. Tieni presente che alcuni di questi ruoli possono essere svolti da una o più aziende.

   L’utente finale dispone di un dispositivo che supporta Adobe AIR. Inoltre, è necessario installare un&#39;applicazione compatibile con UltraViolet. L&#39;applicazione include il codice necessario per analizzare il CFF e presentarlo per l&#39;utilizzo da parte del runtime. Tutte le operazioni di crittografia sensibili vengono gestite nel runtime protetto.
1. L&#39;applicazione può attivare un&#39;aggiunta al dominio per il dispositivo, che interagisce con il coordinatore. Il coordinatore gestisce un archivio diritti, un database utenti e i domini. Il gestore del dominio del coordinatore viene creato utilizzando l’SDK per l’accesso Adobe per implementare le operazioni di aggiunta/uscita dal dominio specifiche per l’accesso Adobe.
1. L’utente può quindi utilizzare l’applicazione per selezionare un video che desidera acquisire dal rivenditore. In genere, il rivenditore fornisce un portale web e gestisce tutte le regole di business.
1. Il rivenditore interagisce quindi con il coordinatore per aggiungere un token di diritti. Il rivenditore reindirizza quindi la richiesta al provider di servizi per il download del contenuto effettivo.
1. Se il dispositivo non dispone ancora di una licenza per il contenuto, attiva una richiesta di licenza utilizzando il CFF. La richiesta include in genere un certificato di dominio, credenziali utente e informazioni sull’applicazione. Il provider di servizi gestisce un server Adobe Access License Server (sviluppato utilizzando l&#39;SDK Adobe Access) che segue le specifiche UltraViolet.
1. La logica di business UltraViolet del provider di servizi interagisce con il coordinatore in base alle esigenze per recuperare il token di diritti appropriato per determinare se è necessario rilasciare una licenza per contenuti.

   La licenza per contenuti è associata al dominio. L&#39;applicazione client può inserire la licenza nel file CFF. Ora è possibile riprodurre il contenuto nell’applicazione, con tutte le regole di protezione e utilizzo gestite dal componente Accesso Adobe in fase di esecuzione.
1. Altri dispositivi e applicazioni di proprietà dello stesso utente finale possono essere registrati presso il coordinatore. Il contenuto può ora essere caricato in altre periferiche di accesso Adobe senza richiedere alcuna transazione esterna.
