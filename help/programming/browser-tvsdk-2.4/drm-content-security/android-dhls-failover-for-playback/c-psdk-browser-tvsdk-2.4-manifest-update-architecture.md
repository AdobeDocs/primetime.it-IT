---
description: Seguono alcune informazioni ed esempi su come il browser TVSDK gestisce i manifesti master aggiornati.
title: Architettura dell'aggiornamento del master-manifest live
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---


# Architettura dell&#39;aggiornamento del master-manifest live{#live-master-manifest-update-architecture}

Seguono alcune informazioni ed esempi su come il browser TVSDK gestisce i manifesti master aggiornati.

Per impostazione predefinita, questa funzione è disattivata. Se l&#39;applicazione lo attiva impostando una frequenza di aggiornamento in minuti, i seguenti passaggi si verificano dopo ogni intervallo di aggiornamento:

1. Il browser TVSDK controlla l&#39;ora e il tag dell&#39;ultima modifica del manifesto master per determinare se il file è stato aggiornato.

   Se sia l’ora che il tag sono cambiati, il file viene considerato come modificato.
1. Il browser TVSDK analizza e analizza il nuovo manifesto e adotta le azioni appropriate in base alla natura dell&#39;aggiornamento.
1. Se il bit rate di riproduzione corrente corrisponde al bit rate del manifesto modificato, il browser TVSDK passa al nuovo profilo.

   Il nuovo profilo potrebbe provenire da un server diverso o dallo stesso server, allo stesso bit rate. In questo caso, la transizione è graduale.
1. Se il bit rate di riproduzione corrente non è più presente nel nuovo manifesto, il browser TVSDK cerca di trovare un bit rate nel profilo corrente che esiste anche nel nuovo manifesto.

   * Se viene trovata una corrispondenza, il lettore passa prima al profilo del bit rate corrispondente nel manifesto esistente e passa al profilo del bit rate corrispondente nel manifesto aggiornato. In questo modo la transizione risulterà fluida.
   * Se non c&#39;è un bit rate in comune tra il manifesto precedente e il nuovo manifesto, o se il browser TVSDK non può passare al bit rate corrispondente, il browser TVSDK passa direttamente al bit rate più basso del nuovo manifesto e utilizza ABR per passare a qualsiasi bit rate consentito in base alla larghezza di banda. Questo può causare un leggero difetto nella riproduzione ma dovrebbe avere un impatto minimo.

1. Se l&#39;aggiornamento ha esito positivo, il browser TVSDK invia un evento `MediaPlayerItemEvent.MASTER_UPDATED` .
1. Se l&#39;aggiornamento non ha esito positivo, la riproduzione continua con la configurazione precedente a questo aggiornamento.

## Esempio 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

I seguenti bit rate sono trasmessi in diretta:

* 500.000
* 900.000
* 2100.000

Il flusso 2100k ha alcuni problemi, quindi deve essere riavviato. Il manifesto principale viene aggiornato per contenere solo 500k e 900k. Poco dopo, gli utenti che guardano questo programma a 2100k sperimenteranno un cambio di bit rate a 900k. Gli utenti che guardano a 900k continuano a guardare a 900k. Successivamente, il flusso 2100k riprende, e viene aggiunto nuovamente nel manifesto principale. Poco dopo, gli utenti che guardano a 900k, e hanno la larghezza di banda, sono passati a 2100k.

### Esempio 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

I seguenti bit rate sono trasmessi in diretta:

* 500.000
* 900.000
* 2100.000

Tutti questi bit rate devono essere riavviati. Ci sono due flussi temporali configurati per questo, a 400k e 1500k. Gli utenti sono passati a 400 k, che è il bit rate più basso della nuova configurazione. Alcuni degli utenti sono passati a 1500k quando la loro larghezza di banda è sufficiente. Successivamente, i tre bit rate vengono riportati di nuovo e il manifest viene aggiornato. Gli utenti tornano automaticamente a guardare a 500k, che è la larghezza di banda più bassa nel manifesto rivisto (originale). Poco dopo, gli utenti passano alla larghezza di banda più elevata (900k o 1200k) consentita dalla loro rete.

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->

