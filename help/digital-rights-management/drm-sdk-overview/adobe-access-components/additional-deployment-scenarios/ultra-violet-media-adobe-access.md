---
seo-title: Supporti UltraViolet e  Adobe Primetime DRM
title: Supporti UltraViolet e  Adobe Primetime DRM
uuid: 7076c0f9-e092-48e4-9118-8a414bd03c7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---


# Supporti UltraViolet e  Adobe Primetime DRM {#ultraviolet-media-and-adobe-primetime-drm}

 Adobe Primetime DRM può essere utilizzato con altre soluzioni di streaming di contenuti di terze parti per configurare un ecosistema di distribuzione dei contenuti multimediali completo e sicuro basato su DRM.

UltraViolet ( [https://www.myuv.com/](https://www.uvvu.com/)) è un sistema di autenticazione dei diritti digitali e di distribuzione basato sul cloud che consente ai consumatori di contenuti di home entertainment digitali di trasmettere e scaricare contenuti acquistati tramite più piattaforme e dispositivi. I contenuti UltraViolet verranno scaricati (o trasmessi in streaming) in un formato di file comune (CFF) utilizzando la crittografia comune (CENC).

È facile configurare un sistema UltraViolet insieme  Adobe Primetime DRM. Il seguente esempio di utilizzo illustra il comportamento del flusso di contenuto:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. Il proprietario del contenuto codifica e crea pacchetti per il contenuto in CFF. Il contenuto del pacchetto viene concesso in licenza a un rivenditore per la distribuzione.
1. Il rivenditore carica il contenuto su un fornitore di servizi digitali, come CDN. Il contenuto è ora disponibile per il download. Tenete presente che alcuni di questi ruoli possono essere giocati da una o più società.

   L&#39;utente finale ha un dispositivo che supporta  Adobe AIR. Inoltre, l&#39;utente deve installare un&#39;applicazione compatibile con UltraViolet. L&#39;applicazione include il codice necessario per analizzare il CFF e presentarlo per l&#39;uso da parte del runtime. Tutte le operazioni di crittografia sensibili vengono gestite nel runtime protetto.
1. L&#39;applicazione può attivare un join di dominio per il dispositivo, che interagisce con il coordinatore. Il coordinatore mantiene un blocco dei diritti, un database utente e domini. Il gestore di dominio del coordinatore è creato utilizzando l&#39;SDK DRM di Primetime per implementare le operazioni di join/uscita del dominio specifiche di Primetime DRM.
1. L&#39;utente può quindi utilizzare l&#39;applicazione per selezionare il video che desidera acquisire dal rivenditore. In genere, il rivenditore fornisce un portale Web e gestisce tutte le logiche aziendali.
1. Il rivenditore interagisce quindi con il coordinatore per aggiungere un token di diritti. Il rivenditore quindi reindirizzerà la richiesta al provider di servizi per il download effettivo del contenuto.
1. Se il dispositivo non dispone ancora di una licenza per il contenuto, attiva una richiesta di licenza tramite il CFF. La richiesta in genere include un certificato di dominio, le credenziali utente e le informazioni sull&#39;applicazione. Il provider di servizi gestisce un server di licenze DRM Primetime (sviluppato utilizzando l&#39;SDK DRM di Primetime) che segue le specifiche UltraViolet.
1. La logica di business UltraViolet del fornitore di servizi interagisce con il coordinatore in base alle esigenze per recuperare il token di diritti appropriato per determinare se una licenza di contenuto deve essere rilasciata.

   La licenza di contenuto è associata al dominio. L&#39;applicazione client può inserire la licenza nel file CFF. Ora è possibile riprodurre il contenuto nell&#39;applicazione, con tutta la protezione e l&#39;implementazione delle regole di utilizzo gestite dal componente DRM di Primetime nel runtime.
1. Altri dispositivi e applicazioni di proprietà dello stesso utente finale possono essere registrati presso il coordinatore. Il contenuto ora può essere caricato in altri dispositivi DRM Primetime senza richiedere alcuna transazione esterna.