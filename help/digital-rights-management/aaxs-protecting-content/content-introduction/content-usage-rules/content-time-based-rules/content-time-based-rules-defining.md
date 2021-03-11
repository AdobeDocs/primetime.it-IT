---
title: Definizione di regole basate sul tempo
description: Definizione di regole basate sul tempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Definizione di regole basate su tempo {#defining-time-based-rules}

Adobe Access utilizza l&#39;&quot;applicazione soft&quot; delle restrizioni di licenza basate sul tempo. Se durante la riproduzione di un video scade un diritto di ora, il comportamento predefinito di Accesso Adobe consiste nel non limitare la riproduzione fino alla successiva creazione dello streaming video (chiamando `Netstream.stop()` e `Netstream.play()`).

Anche se l’imposizione soft è il comportamento predefinito, è possibile abilitare l’applicazione forzata eseguendo una delle seguenti attività:

* Chiedi al lettore video di controllare periodicamente la licenza per assicurarsi che nessuna delle restrizioni di tempo sia scaduta. È possibile eseguire questa operazione chiamando `DRMManager.loadVoucher(LOCAL_ONLY).`Un codice di errore indica che la licenza memorizzata localmente non è più valida.
* Ogni volta che l&#39;utente fa clic sul pulsante Pausa, è possibile registrare la marca temporale del video corrente e quindi chiamare `Netstream.stop().`Quando l&#39;utente fa clic sul pulsante Riproduci, è possibile cercare la posizione registrata e quindi chiamare `Netstream.play()`.

## Data di inizio {#start-date}

Specifica la data successiva alla quale una licenza è valida.

Esempio di utilizzo: Utilizza una data assoluta per rilasciare licenze di contenuto prima della data di disponibilità di un bene o per applicare un periodo di &quot;embargo&quot;.

## Data di fine {#end-date}

Specifica la data successiva alla scadenza della licenza.

Esempio di utilizzo: Utilizza una data di scadenza assoluta per riflettere la fine dei diritti di distribuzione.

## Data di fine relativa {#relative-end-date}

Specifica la data di scadenza della licenza, espressa in relazione alla data del packaging.

Esempio di utilizzo: In un processo di packaging automatizzato, utilizza un singolo criterio con questa opzione per una serie di video per impostare la data di scadenza a 30 giorni rispetto alla data del pacchetto.

## Durata della memorizzazione in cache della licenza {#license-caching-duration}

Specifica la durata per la quale una licenza può essere memorizzata nella cache su disco nell&#39;archivio licenze locale del client senza richiedere la riacquisizione dal server licenze. In alternativa, è possibile specificare una data/ora assoluta dopo la quale una licenza non può più essere memorizzata nella cache.

Una volta passata la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza dal server licenze.

Esempio di utilizzo: Utilizzare la durata del caching delle licenze per specificare un periodo di tempo fisso valido per una determinata licenza, ad esempio in un caso di utilizzo a noleggio. È possibile specificare un noleggio di 30 giorni (con memorizzazione in cache della licenza) per indicare la durata totale della licenza entro la quale consumare il contenuto.

## Finestra di riproduzione {#playback-window}

Specifica la durata della validità di una licenza dopo la prima esecuzione del contenuto protetto.

Esempio di utilizzo: Alcuni modelli commerciali consentono un periodo di noleggio di 30 giorni ma, una volta iniziata la riproduzione, deve essere completata in 48 ore. Questa durata di 48 ore della licenza è definita come la finestra di riproduzione.

## Requisiti per la sincronizzazione {#requirements-for-synchronization}

Specifica la frequenza con cui il client sincronizzerà il proprio stato con il server. Se al client è stata rilasciata una licenza fuori banda (senza contattare un server licenze), le regole di utilizzo possono specificare che il client deve inviare messaggi di sincronizzazione al server al fine di sincronizzare l&#39;orario protetto del client e segnalare lo stato del client al server.

Il comportamento di sincronizzazione viene definito utilizzando i seguenti parametri:

* Intervallo iniziale - Specifica il tempo di attesa dopo l&#39;ultima sincronizzazione riuscita per avviare un&#39;altra richiesta di sincronizzazione.
* Intervallo di arresto rigido — (facoltativo). Disabilitare la riproduzione se la sincronizzazione non si è verificata correttamente nel tempo specificato.
* Forza probabilità di sincronizzazione — (facoltativo). Probabilità con cui il client deve inviare un messaggio di sincronizzazione prima dell’intervallo di avvio successivo.

>[!NOTE]
>
>Questa regola di utilizzo è supportata dai client Adobe Access versione 3.0 e successive. Il comportamento dei client meno recenti dipende dalla versione client minima supportata dal server licenze. Vedere [Versione minima del client](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).