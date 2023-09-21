---
title: Definizione di regole basate sul tempo
description: Definizione di regole basate sul tempo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Definizione di regole basate sul tempo {#defining-time-based-rules}

Adobe Access utilizza l&#39;applicazione temporanea delle restrizioni delle licenze basate sul tempo. Se un diritto di tempo scade durante la riproduzione di un video, il comportamento predefinito di Adobe Access consiste nel non limitare la riproduzione fino alla successiva creazione del flusso video (effettuando una chiamata `Netstream.stop()` e `Netstream.play()`).

Anche se l&#39;imposizione soft è il comportamento predefinito, è possibile abilitare l&#39;imposizione hard eseguendo una delle seguenti attività:

* Chiedi al lettore video di eseguire periodicamente il polling della licenza per assicurarti che nessuna delle restrizioni di tempo sia scaduta. A tale scopo, è possibile chiamare `DRMManager.loadVoucher(LOCAL_ONLY).`Un codice di errore indica che la licenza archiviata localmente non è più valida.
* Ogni volta che l’utente fa clic sul pulsante Pausa, puoi registrare il timestamp del video corrente e quindi chiamare `Netstream.stop().`Quando l’utente fa clic sul pulsante Play, puoi cercare la posizione registrata e quindi chiamare `Netstream.play()`.

## Data di inizio {#start-date}

Specifica la data dopo la quale una licenza è valida.

Caso d’uso di esempio: utilizza una data assoluta per rilasciare licenze per contenuti prima della data di disponibilità di una risorsa o per applicare un periodo di &quot;embargo&quot;.

## Data di fine {#end-date}

Specifica la data dopo la quale scadono le licenze.

Caso d’uso di esempio: utilizza una data di scadenza assoluta per riflettere la fine dei diritti di distribuzione.

## Data di fine relativa {#relative-end-date}

Specifica la data di scadenza della licenza, espressa in relazione alla data di creazione del pacchetto.

Caso d’uso di esempio: in un processo di creazione automatica dei pacchetti, utilizza un singolo criterio con questa opzione per una serie di video per impostare la data di scadenza su 30 giorni rispetto alla data di creazione dei pacchetti.

## Durata caching licenze {#license-caching-duration}

Specifica la durata per la quale una licenza può essere memorizzata nella cache del disco nell&#39;archivio licenze locale del client senza richiedere la riacquisizione dal server licenze. In alternativa, è possibile specificare una data/ora assoluta dopo la quale una licenza non può più essere memorizzata nella cache.

Una volta superata la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza al server licenze.

Caso d’uso di esempio: utilizza la durata di memorizzazione nella cache delle licenze per specificare un periodo di tempo fisso valido per una determinata licenza, ad esempio in un caso d’uso di noleggio. È possibile specificare un noleggio di 30 giorni (con inserimento delle licenze nella cache) per indicare la durata totale della licenza entro la quale utilizzare il contenuto.

## Finestra di riproduzione {#playback-window}

Specifica la durata di validità di una licenza dopo il primo utilizzo per la riproduzione di contenuto protetto.

Caso d’uso di esempio: alcuni modelli aziendali consentono un periodo di noleggio di 30 giorni, ma una volta avviata la riproduzione deve essere completata in 48 ore. La durata di 48 ore della licenza viene definita come intervallo di riproduzione.

## Requisiti per la sincronizzazione {#requirements-for-synchronization}

Specifica la frequenza con cui il client sincronizzerà il proprio stato con il server. Se al client è stata rilasciata una licenza out-of-band (senza contattare il server licenze), le regole di utilizzo possono specificare che il client deve inviare messaggi di sincronizzazione al server per sincronizzare l&#39;ora protetta del client e segnalare lo stato del client al server.

Il comportamento di sincronizzazione viene definito utilizzando i seguenti parametri:

* Intervallo di avvio — specifica il tempo di attesa dopo l&#39;ultima sincronizzazione riuscita per avviare un&#39;altra richiesta di sincronizzazione.
* Intervallo di arresto rigido — (facoltativo). Non consentire la riproduzione se la sincronizzazione non ha avuto esito positivo per il periodo di tempo specificato.
* Forza probabilità di sincronizzazione — (facoltativo). Probabilità con cui il client deve inviare un messaggio di sincronizzazione prima del successivo intervallo di avvio.

>[!NOTE]
>
>Questa regola di utilizzo è supportata dai client Adobe Access versione 3.0 e successive. Il comportamento sui client meno recenti dipende dalla versione minima del client supportata dal server licenze. Vedi, [Versione client minima](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).
