---
description: Un lettore video client o il server manifesto possono interagire con il CRS per ottenere il reimballaggio JIT. Entrambi utilizzano la stessa logica di selezione annunci.
seo-description: Un lettore video client o il server manifesto possono interagire con il CRS per ottenere il reimballaggio JIT. Entrambi utilizzano la stessa logica di selezione annunci.
seo-title: Flussi di lavoro dettagliati per il reimballaggio JIT
title: Flussi di lavoro dettagliati per il reimballaggio JIT
uuid: 11b6eb3c-f6aa-4018-9b20-ab6f5910508b
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Flussi di lavoro dettagliati per il reimballaggio JIT {#detailed-workflows-for-jit-repackaging}

Un lettore video client o il server manifesto possono interagire con il CRS per ottenere il reimballaggio JIT. Entrambi utilizzano la stessa logica di selezione annunci.

## Reimballaggio JIT avviato dal server manifesto {#section_1F1C1B7DD146403890C2B43E24FEF0EB}

![](assets/ssai_JIT-workflow_web.png)

Il flusso di lavoro per la ricompilazione JIT sul lato server manifesto è il seguente:

1. Il server manifest effettua una richiesta al server di annunci.
1. Il server manifesto riceve un annuncio creativo che non è in formato HLS.
1. Il server manifesto invia una richiesta al server CDN per una versione HLS precedentemente transcodificata dell’annuncio creativo.

   >[!NOTE]
   >
   >In una configurazione multi-CDN, il server manifesto utilizza il `ptcdn` parametro nell’URL di avvio per identificare il server CDN.

1. Il server manifesto controlla la risposta:

   1. Se la richiesta ha esito positivo, il server manifesto inserisce nel flusso di contenuto la versione HLS precedentemente transcodificata dell’annuncio creativo.
   1. Se la richiesta ha esito negativo, il server manifesto genera una voce di registro e richiede una versione transcodificata da CRS.

1. CRS transcodifica l’annuncio creativo e carica la versione HLS sul server CDN per un utilizzo futuro.

Per tutte le richieste successive per tale creativo, il server manifesto recupera la versione HLS dalla CDN e la inserisce nel flusso di contenuto.

## Reimballaggio JIT avviato dal client {#section_FBC97D40043F4FDD98247A08BB6195B0}

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

Un client basato su TVSDK o con funzionalità simili può interagire con CRS per ottenere il riconfezionamento JIT, come segue:

1. Il client richiede un annuncio dal server di annunci.
1. Il server annunci restituisce l’annuncio al client.
1. Il client verifica il formato dell&#39;annuncio dal server di annunci:

   1. Se l’annuncio è in formato HLS, il client lo inserisce (punti) nel contenuto e viene fatto.
   1. Se l’annuncio non è in formato HLS, il client ne richiede uno dal server CDN.

      >[!NOTE]
      >
      >In una configurazione multi-CDN, il server manifesto utilizza il `ptcdn` parametro nell’URL di avvio per identificare il server CDN.

1. Il client controlla la risposta dal server CDN.

   1. Se la CDN ha fornito una versione HLS, il client la inserisce (punti) nel contenuto ed è fatto.
   1. Se il server CDN non fornisce una versione HLS, il client chiede al server di annunci di richiederne una da CRS. Il client non inserisce l&#39;annuncio nel contenuto.

1. Il server annunci richiede che l’annuncio non-HLS venga transcodificato in HLS.
1. CRS crea una versione HLS e la carica sul server CDN per un utilizzo futuro.

## Priorità e cronologia del formato annuncio {#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

Il server manifesto e il client utilizzano la stessa logica di selezione per determinare le priorità per la riproduzione degli annunci disponibili. Gli annunci in formato HLS sono la prima priorità, seguiti da MP4, FLV e infine WebM.

Il CRS richiede in genere 2-4 minuti per elaborare un annuncio pubblicitario non HLS, e in genere meno di 3 minuti.

CRS produce bitrate HLS diversi, in modo che l&#39;annuncio possa essere riprodotto a una velocità adeguata alla velocità di connessione e alla larghezza di banda disponibili. Se sono disponibili diversi bitrate, CRS sceglie il bit rate più alto disponibile. Se il CRS riceve un annuncio pubblicitario non HLS, produce una versione HLS alla massima risoluzione disponibile.