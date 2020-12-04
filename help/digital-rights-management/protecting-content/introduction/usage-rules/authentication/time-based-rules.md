---
seo-title: Regole basate sul tempo
title: Regole basate sul tempo
uuid: 19a6ee7e-9580-48bb-a3a6-ff2cedcc796a
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Regole temporizzate {#time-based-rules}

Primetime DRM utilizza l&#39;applicazione &quot;soft&quot; delle restrizioni di licenza basate sull&#39;ora. Se un diritto di ora scade durante la riproduzione di un video, il comportamento predefinito di Primetime DRM non limita la riproduzione fino alla successiva creazione dello streaming video (chiamando `Netstream.stop()` e `Netstream.play()`).

Anche se l&#39;imposizione non restrittiva è il comportamento predefinito, potete anche abilitare l&#39;imposizione forzata eseguendo una delle seguenti operazioni:

* Accertatevi che il lettore video controlli periodicamente la licenza per verificare che nessuna delle limitazioni di tempo sia scaduta. Questo può essere ottenuto chiamando `DRMManager.loadVoucher(LOCAL_ONLY).` Un codice di errore indica che la licenza memorizzata localmente non è più valida.
* Ogni volta che l&#39;utente fa clic su **[!UICONTROL Pause]**, è possibile registrare il timestamp video corrente e chiamare `Netstream.stop()`. Quando l&#39;utente fa clic sul pulsante Riproduci, è possibile cercare la posizione registrata e quindi chiamare `Netstream.play()`.

## Data di inizio {#start-date}

La data di inizio specifica la data dopo la quale una licenza è valida.

Esempio di utilizzo: Utilizza una data assoluta per rilasciare licenze di contenuto prima della data di disponibilità di una risorsa, o per applicare un periodo di &quot;embargo&quot;.

## Data di fine {#end-date}

La data di fine specifica la data successiva alla quale scade una licenza.

Esempio di utilizzo: Utilizzate una data di scadenza assoluta per riflettere la fine dei diritti di distribuzione.

## Data di fine relativa {#relative-end-date}

La data di fine relativa specifica la data di scadenza della licenza, che viene espressa in relazione alla data dell&#39;imballaggio, non in relazione alla data di rilascio della licenza.

Esempio di utilizzo: In un processo di creazione del pacchetto automatizzato, utilizzate un singolo criterio DRM Primetime con questa opzione per una serie di video, per impostare la data di scadenza su 30 giorni rispetto alla data del pacchetto.

## Durata della cache delle licenze{#license-caching-duration}

La durata del caching delle licenze specifica per quanto tempo una licenza può essere memorizzata nella cache su disco nell&#39;archivio licenze locale del client senza che sia necessario riacquisire dal server licenze. In alternativa, è possibile specificare una data e un&#39;ora assolute dopo le quali una licenza non può più essere memorizzata nella cache.

Una volta trascorsa la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza al server licenze.

Esempio di utilizzo: Utilizzare la durata del caching delle licenze per specificare un periodo di tempo fisso valido per una licenza particolare, ad esempio in un caso di utilizzo in affitto. Potete specificare un noleggio di 30 giorni (con memorizzazione nella cache delle licenze) per indicare la durata totale della licenza entro la quale utilizzare il contenuto.

## Finestra di riproduzione {#playback-window}

La finestra di riproduzione specifica la durata della validità di una licenza dopo che è stata utilizzata per riprodurre il contenuto protetto.

Esempio di utilizzo: Alcuni modelli aziendali consentono un periodo di noleggio di 30 giorni, ma, una volta avviata la riproduzione, la riproduzione deve essere completata in 48 ore. In questo caso, la durata di 48 ore della licenza corrisponde alla finestra di riproduzione.

**Dalla versione 5.3 in avanti**  - La finestra di riproduzione supporta anche l&#39;opzione di attivazione o disattivazione dell&#39;arresto rigido, che indica se il contesto di decrittazione per la riproduzione deve interrompersi alla scadenza della finestra di riproduzione (abilitata) o continuare nonostante la scadenza (disabilitata).

>[!NOTE]
>
>L&#39;opzione di arresto rigido non funziona correttamente con la finestra di riproduzione se utilizzata insieme ad essa (la finestra di riproduzione non sarà rispettata). La riproduzione del contenuto con la finestra di riproduzione senza interruzione protetta rispetta i limiti della finestra di riproduzione.