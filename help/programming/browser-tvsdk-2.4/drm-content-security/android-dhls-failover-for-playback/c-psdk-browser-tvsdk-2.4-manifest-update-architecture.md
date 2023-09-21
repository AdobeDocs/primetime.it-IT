---
description: Di seguito sono riportate alcune informazioni ed esempi su come il TVSDK del browser gestisce i manifesti master aggiornati.
title: Architettura di aggiornamento del manifesto principale live
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# Architettura di aggiornamento del manifesto principale live{#live-master-manifest-update-architecture}

Di seguito sono riportate alcune informazioni ed esempi su come il TVSDK del browser gestisce i manifesti master aggiornati.

Per impostazione predefinita, questa funzione è disattivata. Se l&#39;applicazione lo attiva impostando una frequenza di aggiornamento in minuti, dopo ogni intervallo di aggiornamento si verificano i seguenti passaggi:

1. Il TVSDK del browser controlla l&#39;ora e il tag dell&#39;ultima modifica del manifesto master per determinare se il file è stato aggiornato.

   Se sono stati modificati sia l’ora che l’e-mail, il file viene considerato modificato.
1. Il browser TVSDK analizza e analizza il nuovo manifesto e intraprende azioni appropriate in base alla natura dell’aggiornamento.
1. Se la velocità in bit di riproduzione corrente corrisponde alla velocità in bit del manifesto modificato, TVSDK del browser passa al nuovo profilo.

   Il nuovo profilo potrebbe provenire da un server diverso o dallo stesso server, alla stessa velocità bit. In questo caso, la transizione è uniforme.
1. Se la velocità in bit di riproduzione corrente non è più presente nel nuovo manifesto, TVSDK del browser tenta di trovare una velocità in bit nel profilo corrente che esiste anche nel nuovo manifesto.

   * Se viene trovata una corrispondenza, il lettore passa prima al profilo della velocità in bit corrispondente nel manifesto esistente e poi al profilo della velocità in bit corrispondente nel manifesto aggiornato. In questo modo la transizione risulterà fluida.
   * Se non esiste una velocità in comune tra il manifesto precedente e il nuovo manifesto, o se il TVSDK del browser non può passare alla velocità in bit corrispondente, il TVSDK del browser passa direttamente al profilo della velocità in bit più bassa del nuovo manifesto e utilizza ABR per passare a qualsiasi velocità in bit consentita in base alla larghezza di banda. Questo può causare un leggero intoppo nella riproduzione, ma dovrebbe avere un impatto minimo.

1. Se l&#39;aggiornamento ha esito positivo, il TVSDK del browser invia un `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Se l’aggiornamento non riesce, la riproduzione continua con la configurazione da prima di questo aggiornamento.

## Esempio 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

Le velocità di trasmissione in diretta sono le seguenti:

* 500k
* 900k
* 2100k

Il flusso 2100k presenta alcuni problemi, pertanto è necessario riavviarlo. Il manifesto principale viene aggiornato in modo da contenere solo 500k e 900k. Poco dopo, gli utenti che guarderanno questo programma a 2100k sperimenteranno un bit rate switch down a 900k. Gli utenti che guardano a 900k continuano a guardare a 900k. Successivamente, il flusso 2100k riprende e viene aggiunto nuovamente nel manifesto principale. Un po&#39; più tardi, gli utenti che guardano a 900k, e hanno la larghezza di banda, passano a 2100k.

### Esempio 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

Le velocità di trasmissione in diretta sono le seguenti:

* 500k
* 900k
* 2100k

È necessario riavviare tutte queste velocità bit. Ci sono due flussi temporali impostati per questo, a 400k e 1500k. Gli utenti sono passati a 400k, che è il bit rate più basso della nuova configurazione. Alcuni utenti passano a 1500k quando la loro larghezza di banda è sufficiente. Successivamente, viene eseguito il backup delle tre velocità bit e viene aggiornato il manifesto principale. Gli utenti tornano automaticamente a guardare a 500k, che è la larghezza di banda più bassa nel manifesto rivisto (originale). Poco dopo, gli utenti passano alla larghezza di banda più elevata (900k o 1200k) consentita dalla rete.

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->
