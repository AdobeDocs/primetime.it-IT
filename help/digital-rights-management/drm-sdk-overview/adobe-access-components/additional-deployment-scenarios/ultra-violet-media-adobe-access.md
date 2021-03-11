---
title: Supporti UltraViolet e Adobe Primetime DRM
description: Supporti UltraViolet e Adobe Primetime DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---


# Supporti UltraViolet e Adobe Primetime DRM {#ultraviolet-media-and-adobe-primetime-drm}

Adobe Primetime DRM può essere utilizzato con altre soluzioni di streaming dei contenuti di terze parti per configurare un ecosistema di distribuzione dei contenuti multimediali completo e sicuro basato su DRM.

UltraViolet ( [https://www.myuv.com/](https://www.uvvu.com/)) è un sistema di autenticazione digitale dei diritti e distribuzione basato sul cloud che consente ai consumatori di contenuti di home entertainment digitale di inviare e scaricare contenuti acquistati tramite più piattaforme e dispositivi. I contenuti UltraViolet verranno scaricati (o trasmessi in streaming) in un formato file comune (CFF) utilizzando la codifica comune (CENC).

È facile configurare un sistema UltraViolet insieme a Adobe Primetime DRM. Il seguente caso d’uso illustra il comportamento del flusso di contenuto:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. Il proprietario del contenuto codifica e crea un pacchetto per il contenuto in CFF. Il contenuto del pacchetto viene concesso in licenza a un rivenditore per la distribuzione.
1. Il rivenditore carica il contenuto in un provider di servizi digitali, come CDN. Il contenuto è ora disponibile per il download. Tieni presente che alcuni di questi ruoli possono essere eseguiti da una o più aziende.

   L’utente finale dispone di un dispositivo che supporta Adobe AIR. Inoltre, l&#39;utente deve installare un&#39;applicazione compatibile con UltraViolet. L&#39;applicazione include il codice necessario per analizzare il CFF e presentarlo per il consumo da parte del runtime. Tutte le operazioni di crittografia sensibili vengono gestite nel runtime protetto.
1. L’applicazione può attivare un join di dominio per il dispositivo, che interagisce con il coordinatore. Il coordinatore gestisce un blocco dei diritti, un database utenti e domini. Il gestore di domini del coordinatore è generato utilizzando l’SDK DRM di Primetime per implementare le operazioni di join/congedo del dominio specifico di Primetime DRM.
1. L’utente può quindi utilizzare l’applicazione per selezionare un video che desidera acquisire dal rivenditore. In genere, il rivenditore fornisce un portale web e gestisce tutte le logiche aziendali.
1. Il rivenditore interagisce quindi con il coordinatore per aggiungere un token di diritti. Il rivenditore reindirizza quindi la richiesta al provider di servizi per il download effettivo del contenuto.
1. Se il dispositivo non dispone ancora di una licenza per il contenuto, attiva una richiesta di licenza utilizzando il CFF. La richiesta include in genere un certificato di dominio, le credenziali utente e le informazioni sull’applicazione. Il fornitore di servizi gestisce un server di licenze DRM di Primetime (sviluppato utilizzando l&#39;SDK DRM di Primetime) che segue le specifiche UltraViolet.
1. La logica di business UltraViolet del fornitore di servizi interagisce con il coordinatore in base alle necessità per recuperare il token di diritti appropriato per determinare se è necessario rilasciare una licenza di contenuto.

   La licenza del contenuto è associata al dominio . L&#39;applicazione client può inserire la licenza nel file CFF. Il contenuto può ora essere riprodotto nell’applicazione, con tutte le regole di protezione e utilizzo gestite dal componente DRM di Primetime nel runtime.
1. Altri dispositivi e applicazioni di proprietà dello stesso utente finale possono essere registrati presso il coordinatore. Il contenuto può ora essere caricato in altri dispositivi DRM di Primetime senza richiedere alcuna transazione esterna.