---
description: Adobe Access può essere utilizzato con altre soluzioni di streaming di contenuti di terze parti per configurare un ecosistema di distribuzione dei contenuti multimediali completo e sicuro basato su DRM.
seo-description: Adobe Access può essere utilizzato con altre soluzioni di streaming di contenuti di terze parti per configurare un ecosistema di distribuzione dei contenuti multimediali completo e sicuro basato su DRM.
seo-title: Supporti UltraViolet e Adobe Access
title: Supporti UltraViolet e Adobe Access
uuid: d287680f-02de-4cca-aeea-22b7fd8e67d2
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Supporti UltraViolet e Adobe Access {#ultraviolet-media-and-adobe-access}

Adobe Access può essere utilizzato con altre soluzioni di streaming di contenuti di terze parti per configurare un ecosistema di distribuzione dei contenuti multimediali completo e sicuro basato su DRM.

UltraViolet ( [](https://www.uvvu.com/)) è un sistema di autenticazione dei diritti digitali e di distribuzione basato su cloud che consente ai consumatori di contenuti di home entertainment digitali di trasmettere e scaricare contenuti acquistati tramite più piattaforme e dispositivi. I contenuti UltraViolet verranno scaricati (o trasmessi in streaming) in un formato di file comune (CFF) utilizzando la crittografia comune (CENC).

È facile configurare un sistema UltraViolet insieme ad Adobe Access. Il seguente esempio di utilizzo illustra il comportamento del flusso di contenuto:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. Il proprietario del contenuto codifica e crea pacchetti per il contenuto in CFF. Il contenuto del pacchetto viene concesso in licenza a un rivenditore per la distribuzione.
1. Il rivenditore carica il contenuto su un fornitore di servizi digitali, come CDN. Il contenuto è ora disponibile per il download. Tenete presente che alcuni di questi ruoli possono essere giocati da una o più società.

   L&#39;utente finale dispone di un dispositivo che supporta Adobe AIR. Inoltre, l&#39;utente deve installare un&#39;applicazione compatibile con UltraViolet. L&#39;applicazione include il codice necessario per analizzare il CFF e presentarlo per l&#39;uso da parte del runtime. Tutte le operazioni di crittografia sensibili vengono gestite nel runtime protetto.
1. L&#39;applicazione può attivare un join di dominio per il dispositivo, che interagisce con il coordinatore. Il coordinatore mantiene un blocco dei diritti, un database utente e domini. Il gestore di domini del coordinatore è creato utilizzando l’SDK di Adobe Access per implementare le operazioni di partecipazione/uscita del dominio specifiche di Adobe Access.
1. L&#39;utente può quindi utilizzare l&#39;applicazione per selezionare il video che desidera acquisire dal rivenditore. In genere, il rivenditore fornisce un portale Web e gestisce tutte le logiche aziendali.
1. Il rivenditore interagisce quindi con il coordinatore per aggiungere un token di diritti. Il rivenditore quindi reindirizzerà la richiesta al provider di servizi per il download effettivo del contenuto.
1. Se il dispositivo non dispone ancora di una licenza per il contenuto, attiva una richiesta di licenza tramite il CFF. La richiesta in genere include un certificato di dominio, le credenziali utente e le informazioni sull&#39;applicazione. Il provider di servizi gestisce un server di licenze Adobe Access (sviluppato utilizzando l’SDK di Adobe Access) che segue le specifiche di UltraViolet.
1. La logica di business UltraViolet del fornitore di servizi interagisce con il coordinatore in base alle esigenze per recuperare il token di diritti appropriato per determinare se una licenza di contenuto deve essere rilasciata.

   La licenza di contenuto è associata al dominio. L&#39;applicazione client può inserire la licenza nel file CFF. Ora è possibile riprodurre il contenuto nell&#39;applicazione, con tutta la protezione e l&#39;implementazione delle regole di utilizzo gestite dal componente Adobe Access in fase di esecuzione.
1. Altri dispositivi e applicazioni di proprietà dello stesso utente finale possono essere registrati presso il coordinatore. È ora possibile caricare il contenuto in altri dispositivi Adobe Access senza che sia necessaria alcuna transazione esterna.

