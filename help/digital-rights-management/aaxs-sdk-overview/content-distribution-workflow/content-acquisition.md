---
title: Acquisizione di contenuti
description: Acquisizione di contenuti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Acquisizione di contenuti {#content-acquisition}

Quando un consumatore acquisisce un file di contenuto protetto da un sito web o da una rete CDN, deve anche acquisire una licenza che contenga una chiave per decrittografare il video prima di poterlo riprodurre. I passaggi seguenti illustrano un flusso di lavoro comune per determinare in che modo un computer che esegue un Flash Player o Adobe AIR accede al contenuto protetto:

1. Il consumatore visita il sito web del rivenditore e seleziona un video da guardare. Il consumatore tenta di scaricare o inviare il video protetto al proprio computer utilizzando un Flash Player o un&#39;applicazione Adobe AIR.

   Se questa è la prima volta che il consumatore ha tentato di accedere al contenuto protetto utilizzando questo computer specifico, il runtime di Flash Player o Adobe AIR deve prima essere individualizzato come descritto nel passaggio 2. Se il client runtime è già stato personalizzato, il processo di acquisizione di una licenza avviene come descritto nel passaggio 3.

1. Il client runtime Flash Player o Adobe AIR acquisisce un certificato digitale univoco (denominato *certificato macchina*) da un server ospitato da un Adobe.

   Questo processo di assegnazione di un certificato univoco si chiama *individualizzazione*. Individualizzazione identifica in modo univoco sia il computer che il runtime Flash Player o Adobe AIR utilizzato per la riproduzione del contenuto.

   Il processo di individualizzazione consente di associare le licenze scaricate a un computer specifico in cui è installato il client. A ogni computer viene assegnata una credenziale computer univoca (chiave privata del computer e certificato del computer). Se un cliente specifico dovesse essere compromesso, può essere revocato e impedito l’acquisizione di licenze per nuovi contenuti.

1. Il client analizza il contenuto protetto mentre inizia a scaricare o a trasmettere in streaming al computer del consumatore ed estrae l’URL del server licenze del rivenditore dai metadati DRM incorporati nel file.

   I metadati DRM sono tipicamente separati dal contenuto, ad esempio incorporati in un file manifest associato o come BLOB binario, ma possono anche essere incorporati nel file di contenuto. Il client contatta il server licenze all’URL specificato e acquisisce una licenza (come descritto di seguito nel passaggio 4).
1. Il client acquisisce una licenza dal server licenze del rivenditore.

   Durante l&#39;acquisizione della licenza, il client invia al server licenze del rivenditore informazioni che identificano il contenuto richiesto (i *metadati DRM*) e il certificato del computer (che identifica il computer del consumatore). La richiesta di licenza inviata al server viene crittografata utilizzando la chiave pubblica di trasporto, che è inclusa anche nei metadati DRM.

   Il server licenze, che può essere integrato nell&#39;infrastruttura di fatturazione e autenticazione del rivenditore, può eseguire un controllo delle regole aziendali per verificare che l&#39;utente sia autorizzato a visualizzare il contenuto richiesto. Se le regole business lo consentono, il server licenze rilascia una licenza contenente la chiave di crittografia del contenuto per decrittografare il contenuto e le regole di utilizzo associate all’account dell’utente. Per elaborare una richiesta di licenza, il server licenze decrittografa la richiesta utilizzando la relativa chiave privata Transport. La CEK nei metadati viene decrittografata utilizzando la chiave privata del server licenze e crittografata nuovamente per associare la licenza al dispositivo che effettua la richiesta. La licenza viene firmata utilizzando la chiave privata del server licenze. La risposta alla licenza viene firmata utilizzando la chiave privata di trasporto e crittografata prima di essere restituita al client.

   Se consentito dalla licenza, il client memorizza la licenza per abilitare *l&#39;accesso offline* alla licenza. Il caching delle licenze consente al consumatore di visualizzare il contenuto protetto senza riacquisire una licenza ogni volta che desidera visualizzare il contenuto.

1. Una volta che il client runtime di Flash Player o Adobe AIR dispone di una licenza, il client estrae la CEK dalla licenza e il consumatore può visualizzare il contenuto a cui è autorizzato l’accesso.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   L’esempio precedente mostra solo un possibile flusso di lavoro. In alternativa, puoi utilizzare un flusso di lavoro con un download proattivo di contenuti in cui l’acquisizione della licenza avviene molto più tardi. Un’altra opzione consiste nell’implementare un flusso di lavoro di pre-ordine in cui si verifica l’acquisizione della licenza prima dell’accesso al contenuto.

