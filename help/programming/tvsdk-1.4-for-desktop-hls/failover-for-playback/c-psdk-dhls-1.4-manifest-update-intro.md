---
description: TVSDK è in grado di rilevare le informazioni di riproduzione modificate nei manifesti m3u8 master per lo streaming live e aggiornare le informazioni di riproduzione durante la riproduzione del flusso. TVSDK supporta un set dinamico di profili di bitrate man mano che i profili appaiono o scompaiono dal manifest principale, compresi i bitrate di profilo non sovrapposti tra gli aggiornamenti.
seo-description: TVSDK è in grado di rilevare le informazioni di riproduzione modificate nei manifesti m3u8 master per lo streaming live e aggiornare le informazioni di riproduzione durante la riproduzione del flusso. TVSDK supporta un set dinamico di profili di bitrate man mano che i profili appaiono o scompaiono dal manifest principale, compresi i bitrate di profilo non sovrapposti tra gli aggiornamenti.
seo-title: Aggiornamento Live Master-manifest
title: Aggiornamento Live Master-manifest
uuid: 44f8adc2-0538-4c5d-8e39-55f661d8540b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Aggiornamento Live Master-manifest{#live-master-manifest-update}

TVSDK è in grado di rilevare le informazioni di riproduzione modificate nei manifesti m3u8 master per lo streaming live e aggiornare le informazioni di riproduzione durante la riproduzione del flusso. TVSDK supporta un set dinamico di profili di bitrate man mano che i profili appaiono o scompaiono dal manifest principale, compresi i bitrate di profilo non sovrapposti tra gli aggiornamenti.

Sono supportate le seguenti funzionalità:

* Conteggio profili (crescente o decrescente)
* Bitrate del profilo (sovrapposizione o non sovrapposizione)
* Profili con URL sullo stesso server (o su server diversi)
* Qualsiasi struttura di failover

Devono essere soddisfatte tutte le seguenti condizioni:

* Il flusso è live.
* Sia il tempo che il tag cambiano.
* Tutte le informazioni sul rendering rimangono invariate (con la differenza che gli URL possono variare).
* Le informazioni di accesso DRM restano invariate.
* I segmenti sono racchiusi tra gli stessi PTS e i bordi dei fotogrammi in un piccolo intervallo di errore.

## Architettura di aggiornamento master-manifest dal vivo {#section_32254A0F684B4960ACC33BF6B1AEF6F1}

Di seguito sono riportati alcuni esempi e informazioni su come TVSDK può contenere i manifesti principali aggiornati.

Per impostazione predefinita, questa funzione è disattivata. Se l&#39;applicazione la attiva impostando una frequenza di aggiornamento in minuti, dopo ogni intervallo di aggiornamento si verificano i seguenti passaggi:

1. TVSDK controlla l&#39;ora e il tag dell&#39;ultima modifica del manifesto master per determinare se il file è stato aggiornato.

   Se sia l’ora che il tag sono cambiati, il file viene considerato come modificato.
1. TVSDK analizza e analizza il nuovo manifesto e prende le azioni appropriate in base alla natura dell&#39;aggiornamento.
1. Se il bitrate di riproduzione corrente corrisponde al bitrate del manifesto modificato, TVSDK passa al nuovo profilo.

   Il nuovo profilo potrebbe provenire da un server diverso o dallo stesso server, con lo stesso bitrate. In questo caso, la transizione è uniforme.
1. Se il bitrate di riproduzione corrente non è più presente nel nuovo manifesto, TVSDK tenta di trovare un bitrate nel profilo corrente che esiste anche nel nuovo manifesto.

   * Se viene trovata una corrispondenza, il lettore passa innanzitutto al profilo di bitrate corrispondente nel manifesto esistente e passa al profilo di bitrate corrispondente nel manifesto aggiornato. In questo modo la transizione risulterà fluida.
   * Se non esiste un bitrate in comune tra il manifesto precedente e il nuovo manifesto, o se TVSDK non è in grado di passare al bitrate corrispondente, TVSDK passa direttamente al profilo del bitrate più basso del nuovo manifesto e utilizza ABR per passare a qualsiasi bitrate consentito in base alla larghezza di banda. Questo può causare un leggero difetto di riproduzione, ma dovrebbe avere un impatto minimo.

1. Se l’aggiornamento ha esito positivo, TVSDK invia un `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Se l&#39;aggiornamento non riesce, la riproduzione continua con la configurazione precedente a questo aggiornamento.

### Esempio 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

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

## Usa aggiornamento live master-manifest {#section_34AC4A9751DB4B7C8561302C6A59A1C4}

Potete attivare questa funzione e verificare la presenza di eventi correlati.

1. Per attivare gli aggiornamenti Live Master-manifest, imposta la frequenza di aggiornamento (in minuti) impostando la `NetworkConfiguration.masterUpdateInterval` proprietà.
1. Facoltativamente, potete tenere traccia degli aggiornamenti del manifesto riusciti ascoltando l&#39; `MediaPlayerItemEvent.MASTER_UPDATED` evento.

