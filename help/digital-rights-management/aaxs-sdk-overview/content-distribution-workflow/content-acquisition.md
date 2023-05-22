---
title: Acquisizione dei contenuti
description: Acquisizione dei contenuti
copied-description: true
exl-id: 661bc6a1-34b6-4e0d-afbd-76f701728297
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Acquisizione dei contenuti {#content-acquisition}

Quando un consumatore acquisisce un file di contenuto protetto da un sito web o da una rete CDN, deve anche acquisire una licenza che contenga una chiave per decrittografare il video prima che possa essere riprodotto. I passaggi seguenti illustrano un flusso di lavoro comune per la modalità di accesso ai contenuti protetti da parte di un computer che esegue un Flash Player o Adobe AIR:

1. Il consumatore visita il sito web del rivenditore e seleziona un video da guardare. Il consumatore tenta di scaricare o inviare in streaming il video protetto sul proprio computer utilizzando un Flash Player o un’applicazione Adobe AIR.

   Se è la prima volta che il consumatore tenta di accedere a contenuti protetti utilizzando questo computer specifico, il Flash Player o il runtime di Adobe AIR devono prima essere personalizzati, come descritto nel passaggio 2. Se il client di runtime è già stato personalizzato, il processo di acquisizione di una licenza viene eseguito come descritto nel passaggio 3.

1. Il client runtime di Flash Player o Adobe AIR acquisisce un certificato digitale univoco (denominato *certificato computer*) da un server ospitato da Adobe.

   Questo processo di assegnazione di un certificato univoco è denominato *individualizzazione*. La personalizzazione identifica in modo univoco sia il computer che il runtime di Flash Player o Adobe AIR utilizzato per riprodurre il contenuto.

   Il processo di personalizzazione consente di associare le licenze scaricate a un computer specifico in cui è installato il client. A ogni computer vengono assegnate credenziali di computer univoche (chiave privata del computer e certificato del computer). Se uno specifico cliente viene compromesso, può essere revocato e non può acquisire licenze per nuovi contenuti.

1. Il client analizza il contenuto protetto mentre inizia il download o lo streaming sul computer del consumatore ed estrae l’URL del server licenze del rivenditore dai metadati DRM incorporati nel file.

   I metadati DRM sono in genere separati dal contenuto, ad esempio incorporati in un file manifesto associato o come BLOB binario, ma possono anche essere incorporati all’interno del file di contenuto. Il client contatta il server licenze all’URL specificato e acquisisce una licenza (come descritto di seguito nel passaggio 4).
1. Il client acquisisce una licenza dal server licenze del rivenditore.

   Durante l’acquisizione della licenza, il client invia informazioni che identificano il contenuto richiesto (il *Metadati DRM*) e il certificato del computer (che identifica il computer del consumatore) al server licenze del rivenditore. La richiesta di licenza inviata al server viene crittografata utilizzando la chiave pubblica di trasporto, inclusa anche nei metadati DRM.

   Il server licenze, che può essere integrato nell&#39;infrastruttura di fatturazione e autenticazione del rivenditore, può eseguire un controllo delle regole aziendali per verificare che l&#39;utente sia autorizzato a visualizzare il contenuto richiesto. Se le regole aziendali lo consentono, il server licenze rilascia una licenza contenente la chiave di crittografia del contenuto per decrittografare il contenuto e le regole di utilizzo associate all’account dell’utente. Per elaborare una richiesta di licenza, il server licenze decrittografa la richiesta utilizzando la relativa chiave privata Transport. Il codice CEK nei metadati viene decrittografato utilizzando la chiave privata del server licenze e ricrittografato per associare la licenza al dispositivo che effettua la richiesta. La licenza viene firmata utilizzando la chiave privata del server licenze. La risposta della licenza viene firmata utilizzando la chiave privata di trasporto e crittografata prima di essere restituita al client.

   Se consentito dalla licenza, il client memorizza la licenza per abilitare *accesso offline* alla licenza. La memorizzazione nella cache delle licenze consente al consumatore di visualizzare il contenuto protetto senza dover riacquistare una licenza ogni volta che desidera visualizzare il contenuto.

1. Una volta che il Flash Player o il client runtime di Adobe AIR ha una licenza, il client estrae il CEK dalla licenza e il consumatore può visualizzare il contenuto a cui è autorizzato ad accedere.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   L’esempio precedente mostra un solo flusso di lavoro possibile. In alternativa, puoi utilizzare un flusso di lavoro con download proattivo dei contenuti, in cui l’acquisizione della licenza avviene molto più tardi. Un’altra opzione consiste nell’implementare un flusso di lavoro di pre-ordine in cui l’acquisizione della licenza avviene prima dell’accesso al contenuto.
