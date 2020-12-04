---
seo-title: Definizione di regole basate sul tempo
title: Definizione di regole basate sul tempo
uuid: 17c69869-ac81-4561-9fb6-b1c5c9c4006d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Definizione di regole temporizzate {#defining-time-based-rules}

 Adobe Access utilizza l&#39;applicazione non restrittiva delle restrizioni di licenza basate su tempo. Se un diritto di ora scade durante la riproduzione di un video, il comportamento predefinito di  Accesso Adobe consiste nel non limitare la riproduzione fino alla successiva creazione dello streaming video (chiamando `Netstream.stop()` e `Netstream.play()`).

Anche se l&#39;imposizione non restrittiva è il comportamento predefinito, potete anche abilitare l&#39;imposizione forzata eseguendo una delle seguenti operazioni:

* Accertatevi che il lettore video controlli periodicamente la licenza per verificare che nessuna delle limitazioni di tempo sia scaduta. Questo può essere ottenuto chiamando `DRMManager.loadVoucher(LOCAL_ONLY).`Un codice di errore indica che la licenza memorizzata localmente non è più valida.
* Ogni volta che l&#39;utente fa clic sul pulsante Pausa, è possibile registrare la marca temporale del video corrente e chiamare `Netstream.stop().`Quando l&#39;utente fa clic sul pulsante Riproduci, è possibile cercare la posizione registrata e quindi chiamare `Netstream.play()`.

## Data di inizio {#start-date}

Specifica la data dopo la quale una licenza è valida.

Esempio di utilizzo: Utilizza una data assoluta per rilasciare licenze di contenuto prima della data di disponibilità di una risorsa, o per applicare un periodo di &quot;embargo&quot;.

## Data di fine {#end-date}

Specifica la data di scadenza delle licenze.

Esempio di utilizzo: Utilizzate una data di scadenza assoluta per riflettere la fine dei diritti di distribuzione.

## Data di fine relativa {#relative-end-date}

Specifica la data di scadenza della licenza, espressa in relazione alla data del package.

Esempio di utilizzo: In un processo di creazione automatica del pacchetto, utilizzate un singolo criterio con questa opzione per una serie di video per impostare la data di scadenza su 30 giorni rispetto alla data del pacchetto.

## Durata della cache delle licenze {#license-caching-duration}

Specifica la durata per la quale una licenza può essere memorizzata nella cache su disco nell&#39;archivio licenze locale del client senza che sia necessario riacquisire dal server licenze. In alternativa, potete specificare una data/ora assoluta dopo la quale una licenza non può più essere memorizzata nella cache.

Una volta trascorsa la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza al server licenze.

Esempio di utilizzo: Utilizzare la durata del caching delle licenze per specificare un periodo di tempo fisso valido per una licenza particolare, ad esempio in un caso di utilizzo in affitto. È possibile specificare un noleggio di 30 giorni (con memorizzazione nella cache delle licenze) per indicare la durata totale della licenza entro la quale consumare il contenuto.

## Finestra di riproduzione {#playback-window}

Specifica la durata di validità di una licenza dopo la prima esecuzione del contenuto protetto.

Esempio di utilizzo: Alcuni modelli di business consentono un periodo di noleggio di 30 giorni ma, una volta avviata la riproduzione, deve essere completato in 48 ore. La durata di 48 ore della licenza è definita come finestra di riproduzione.

## Requisiti per la sincronizzazione {#requirements-for-synchronization}

Specifica la frequenza con cui il client sincronizzerà il proprio stato con il server. Se al client è stata rilasciata una licenza fuori banda (senza contattare un server licenze), le regole di utilizzo potrebbero specificare che il client deve inviare messaggi di sincronizzazione al server al fine di sincronizzare l&#39;ora protetta del client e lo stato del client del report al server.

Il comportamento di sincronizzazione è definito utilizzando i seguenti parametri:

* Intervallo iniziale — Specifica quanto tempo attendere dopo l’ultima sincronizzazione per avviare un’altra richiesta di sincronizzazione.
* Intervallo di arresto rigido — (Facoltativo). Disattiva la riproduzione se la sincronizzazione non ha avuto esito positivo nel tempo specificato.
* Forza probabilità di sincronizzazione — (Facoltativo). Probabilità con cui il client deve inviare un messaggio di sincronizzazione prima del successivo intervallo di inizio.

>[!NOTE]
>
>Questa regola di utilizzo è supportata  client di accesso al Adobe versione 3.0 e successive. Il comportamento dei client meno recenti dipende dalla versione client minima supportata dal server licenze. Vedere [Versione minima del client](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).