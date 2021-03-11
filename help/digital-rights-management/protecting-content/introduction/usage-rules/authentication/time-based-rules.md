---
title: Regole basate sul tempo
description: Regole basate sul tempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Regole basate sul tempo {#time-based-rules}

Primetime DRM utilizza l’&quot;applicazione morbida&quot; delle restrizioni delle licenze basate sul tempo. Se durante la riproduzione di un video scade un diritto di tempo, il comportamento predefinito di Primetime DRM è quello di non limitare la riproduzione fino alla successiva creazione dello streaming video (chiamando `Netstream.stop()` e `Netstream.play()`).

Anche se l’imposizione soft è il comportamento predefinito, è possibile abilitare l’applicazione forzata eseguendo una delle seguenti attività:

* Chiedi al lettore video di controllare periodicamente la licenza per assicurarsi che nessuna delle restrizioni di tempo sia scaduta. Puoi eseguire questa operazione chiamando `DRMManager.loadVoucher(LOCAL_ONLY).` Un codice di errore indica che la licenza memorizzata localmente non è più valida.
* Ogni volta che l&#39;utente fa clic su **[!UICONTROL Pause]**, è possibile registrare la marca temporale del video corrente e quindi chiamare `Netstream.stop()`. Quando l&#39;utente fa clic sul pulsante Play, è possibile cercare la posizione registrata e quindi chiamare `Netstream.play()`.

## Data di inizio {#start-date}

La data di inizio specifica la data successiva alla quale una licenza è valida.

Esempio di utilizzo: Utilizza una data assoluta per rilasciare licenze di contenuto prima della data di disponibilità di un bene o per applicare un periodo di &quot;embargo&quot;.

## Data di fine {#end-date}

La data di fine specifica la data successiva alla scadenza della licenza.

Esempio di utilizzo: Utilizza una data di scadenza assoluta per riflettere la fine dei diritti di distribuzione.

## Data di fine relativa {#relative-end-date}

La data di fine relativa specifica la data di scadenza della licenza, espressa in relazione alla data dell’imballaggio, non in relazione alla data di rilascio della licenza.

Esempio di utilizzo: In un processo di packaging automatizzato, utilizza un singolo criterio DRM Primetime con questa opzione per una serie di video, per impostare la data di scadenza a 30 giorni rispetto alla data del packaging.

## Durata della memorizzazione in cache della licenza{#license-caching-duration}

La durata del caching delle licenze specifica per quanto tempo una licenza può essere memorizzata nella cache su disco nell&#39;archivio licenze locale del client senza richiedere la riacquisizione dal server licenze. In alternativa, è possibile specificare una data e un’ora assolute dopo le quali una licenza non può più essere memorizzata nella cache.

Una volta passata la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza dal server licenze.

Esempio di utilizzo: Utilizzare la durata del caching delle licenze per specificare un periodo di tempo fisso valido per una determinata licenza, ad esempio in un caso di utilizzo a noleggio. È possibile specificare un noleggio di 30 giorni (con memorizzazione in cache della licenza) per indicare la durata totale della licenza entro cui utilizzare il contenuto.

## Finestra di riproduzione {#playback-window}

La finestra di riproduzione specifica la durata della validità di una licenza dopo la prima riproduzione di contenuto protetto.

Esempio di utilizzo: Alcuni modelli commerciali consentono un periodo di noleggio di 30 giorni ma, una volta iniziata la riproduzione, la riproduzione deve essere completata in 48 ore. In questo caso, la durata di 48 ore della licenza è la finestra di riproduzione.

**Dalla versione 5.3 in avanti**  - La finestra di riproduzione supporta anche l&#39;opzione di abilitare o disabilitare l&#39;hard Stop, che indica se il contesto di decrittografia per la riproduzione deve arrestarsi alla scadenza della finestra di riproduzione (abilitata) o continuare nonostante la scadenza (disabilitata).

>[!NOTE]
>
>L&#39;opzione hard stop non funziona correttamente con la finestra di riproduzione se utilizzata insieme ad essa (la finestra di riproduzione non verrà rispettata). La riproduzione di contenuto con la finestra di riproduzione senza arresto sicuro rispetta le limitazioni della finestra di riproduzione.