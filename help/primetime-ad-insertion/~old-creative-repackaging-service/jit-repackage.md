---
description: Un lettore video client o il server manifest possono interagire con CRS per ottenere il riconfezionamento JIT. Entrambi utilizzano la stessa logica di selezione degli annunci.
title: Flussi di lavoro dettagliati per il repackaging JIT
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Flussi di lavoro dettagliati per il repackaging JIT {#detailed-workflows-for-jit-repackaging}

Un lettore video client o il server manifest possono interagire con CRS per ottenere il riconfezionamento JIT. Entrambi utilizzano la stessa logica di selezione degli annunci.

## Repackaging JIT avviato dal server manifesto {#section_1F1C1B7DD146403890C2B43E24FEF0EB}

![](assets/ssai_JIT-workflow_web.png)

Il flusso di lavoro per il riconfezionamento JIT sul lato server manifesto è il seguente:

1. Il server manifest effettua una richiesta al server di annunci.
1. Il server manifesto riceve un annuncio creativo che non è in formato HLS.
1. Il server manifest invia una richiesta al server CDN per una versione HLS precedentemente transcodificata dell&#39;annuncio creativo.

   >[!NOTE]
   >
   >In una configurazione multi-CDN, il server manifesto utilizza il parametro `ptcdn` nell&#39;URL di avvio per identificare il server CDN.

1. Il server manifest controlla la risposta:

   1. Se la richiesta ha esito positivo, il server manifest inserisce nel flusso di contenuto la versione HLS precedentemente transcodificata dell&#39;annuncio creativo.
   1. Se la richiesta non riesce, il server manifest genera una voce di registro e richiede una versione transcodificata da CRS.

1. CRS transcodifica l’annuncio creativo e carica la versione HLS sul server CDN per un utilizzo futuro.

Per tutte le richieste successive per tale creativo, il server manifesto recupera la versione HLS dalla CDN e la inserisce nel flusso di contenuto.

## Repackaging JIT avviato dal client {#section_FBC97D40043F4FDD98247A08BB6195B0}

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

Un client basato su TVSDK o con funzionalità simili può interagire con CRS per ottenere il riconfezionamento JIT, come segue:

1. Il client richiede un annuncio dal server di annunci.
1. Il server di annunci restituisce l&#39;annuncio al client.
1. Il client controlla il formato dell&#39;annuncio dal server dell&#39;annuncio:

   1. Se l’annuncio è in formato HLS, il client lo inserisce (unisce) nel contenuto e viene fatto.
   1. Se il contenuto creativo dell’annuncio non è in formato HLS, il client ne richiede uno dal server CDN.

      >[!NOTE]
      >
      >In una configurazione multi-CDN, il server manifesto utilizza il parametro `ptcdn` nell&#39;URL di avvio per identificare il server CDN.

1. Il client controlla la risposta dal server CDN.

   1. Se la CDN ha fornito una versione HLS, il client lo inserisce (unisce) nel contenuto e viene fatto.
   1. Se il server CDN non fornisce una versione HLS, il client richiede al server di annunci di richiederne una da CRS. Il client non inserisce l’annuncio nel contenuto.

1. Il server di annunci richiede la transcodifica dell’annuncio non HLS in HLS.
1. CRS crea una versione HLS e la carica sul server CDN per un utilizzo futuro.

## Priorità e timeline del formato annuncio {#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

Il server manifest e il client utilizzano la stessa logica di selezione per determinare le priorità per la riproduzione degli annunci disponibili. Gli annunci in formato HLS sono la prima priorità, seguiti da MP4, FLV e infine WebM.

CRS richiede in genere 2-4 minuti per elaborare un annuncio non HLS e creativo, e di solito meno di 3 minuti.

CRS produce diversi bit rate HLS, in modo che l&#39;annuncio possa essere riprodotto a una velocità adeguata alla velocità di connessione e alla larghezza di banda disponibili. Se sono disponibili più bit rate, CRS sceglie il bit rate più alto disponibile. Se il CRS riceve un annuncio non HLS creativo, produce una versione HLS alla massima risoluzione disponibile.