---
description: Di seguito sono riportati alcuni esempi e informazioni su come il Browser TVSDK contiene i manifesti principali aggiornati.
seo-description: Di seguito sono riportati alcuni esempi e informazioni su come il Browser TVSDK contiene i manifesti principali aggiornati.
seo-title: Architettura di aggiornamento master-manifest dal vivo
title: Architettura di aggiornamento master-manifest dal vivo
uuid: 6f253502-8dec-4b42-9ee1-99ad9bfd6080
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Architettura di aggiornamento master-manifest dal vivo{#live-master-manifest-update-architecture}

Di seguito sono riportati alcuni esempi e informazioni su come il Browser TVSDK contiene i manifesti principali aggiornati.

Per impostazione predefinita, questa funzione è disattivata. Se l&#39;applicazione la attiva impostando una frequenza di aggiornamento in minuti, dopo ogni intervallo di aggiornamento si verificano i seguenti passaggi:

1. Il Browser TVSDK controlla l&#39;ora e il tag dell&#39;ultima modifica del manifesto master per determinare se il file è stato aggiornato.

   Se sia l’ora che il tag sono cambiati, il file viene considerato come modificato.
1. Il browser TVSDK analizza e analizza il nuovo manifesto ed esegue le azioni appropriate in base alla natura dell&#39;aggiornamento.
1. Se il bitrate di riproduzione corrente corrisponde al bitrate del manifesto modificato, il browser TVSDK passa al nuovo profilo.

   Il nuovo profilo potrebbe provenire da un server diverso o dallo stesso server, con lo stesso bitrate. In questo caso, la transizione è uniforme.
1. Se il bitrate di riproduzione corrente non è più presente nel nuovo manifesto, il browser TVSDK tenta di trovare nel profilo corrente un bitrate che esiste anche nel nuovo manifesto.

   * Se viene trovata una corrispondenza, il lettore passa innanzitutto al profilo di bitrate corrispondente nel manifesto esistente e passa al profilo di bitrate corrispondente nel manifesto aggiornato. In questo modo la transizione risulterà fluida.
   * Se non esiste un bitrate in comune tra il manifesto precedente e il nuovo manifesto, o se il browser TVSDK non è in grado di passare al bitrate corrispondente, il browser TVSDK passa direttamente al profilo del bitrate più basso del nuovo manifesto e utilizza ABR per passare a qualsiasi bitrate consentito in base alla larghezza di banda. Questo può causare un leggero difetto di riproduzione, ma dovrebbe avere un impatto minimo.

1. Se l&#39;aggiornamento ha esito positivo, il Browser TVSDK invia un `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Se l&#39;aggiornamento non riesce, la riproduzione continua con la configurazione precedente a questo aggiornamento.

## Esempio 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

I seguenti bitrate sono la trasmissione live:

* 500k
* 900k
* 2100k

Il flusso 2100k presenta alcuni problemi, quindi deve essere riavviato. Il manifesto principale viene aggiornato in modo da contenere solo 500k e 900k. Poco dopo, gli utenti che guardano questo programma a 2100k sperimenteranno un cambio di bit rate a 900k. Gli utenti che guardano a 900k continuano a guardare a 900k. Successivamente, il flusso 2100k riprende e viene aggiunto nuovamente nel manifesto principale. Poco dopo, gli utenti che guardano a 900k, e hanno la larghezza di banda, sono passati a 2100k.

### Esempio 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

I seguenti bitrate sono la trasmissione live:

* 500k
* 900k
* 2100k

È necessario riavviare tutti questi bit rate. Ci sono due flussi temporali configurati per questo, a 400k e 1500k. Gli utenti passano a 400 k, il bit rate più basso della nuova configurazione. Alcuni utenti passano a 1500 k quando la larghezza di banda è sufficiente. In seguito, i tre bitrate vengono riprodotti e il manifesto master viene aggiornato. Gli utenti tornano automaticamente a guardare a 500k, che è la larghezza di banda più bassa nel manifesto rivisto (originale). Poco dopo, gli utenti passano alla larghezza di banda più elevata (900k o 1200k) consentita dalla rete.

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->

