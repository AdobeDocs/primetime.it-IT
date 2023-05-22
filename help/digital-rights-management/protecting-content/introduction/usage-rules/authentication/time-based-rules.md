---
title: Regole basate sul tempo
description: Regole basate sul tempo
copied-description: true
exl-id: 02a5c10d-13f5-4482-b525-bf6a1ec9dcf0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Regole basate sul tempo {#time-based-rules}

Primetime DRM utilizza l&#39;applicazione flessibile delle restrizioni delle licenze basate sul tempo. Se un diritto di tempo scade durante la riproduzione di un video, il comportamento predefinito di Primetime DRM consiste nel non limitare la riproduzione fino alla successiva creazione del flusso video (effettuando una chiamata `Netstream.stop()` e `Netstream.play()`).

Anche se l&#39;imposizione soft è il comportamento predefinito, è possibile abilitare l&#39;imposizione hard eseguendo una delle seguenti attività:

* Chiedi al lettore video di eseguire periodicamente il polling della licenza per assicurarti che nessuna delle restrizioni di tempo sia scaduta. A tale scopo, è possibile chiamare `DRMManager.loadVoucher(LOCAL_ONLY).` Un codice di errore indica che la licenza archiviata localmente non è più valida.
* Quando l’utente fa clic su **[!UICONTROL Pause]**, puoi registrare la marca temporale del video corrente e quindi chiamare `Netstream.stop()`. Quando l’utente fa clic sul pulsante Play, puoi cercare la posizione registrata e quindi chiamare `Netstream.play()`.

## Data di inizio {#start-date}

La data di inizio specifica la data dopo la quale una licenza è valida.

Caso d’uso di esempio: utilizza una data assoluta per rilasciare licenze per contenuti prima della data di disponibilità di una risorsa o per applicare un periodo di &quot;embargo&quot;.

## Data di fine {#end-date}

La data di fine specifica la data dopo la quale scade una licenza.

Caso d’uso di esempio: utilizza una data di scadenza assoluta per riflettere la fine dei diritti di distribuzione.

## Data di fine relativa {#relative-end-date}

La data di fine relativa specifica la data di scadenza della licenza, che è espressa in relazione alla data di imballaggio, non in relazione alla data di rilascio della licenza.

Caso d’uso di esempio: in un processo di creazione automatica dei pacchetti, utilizza un singolo criterio DRM di Primetime con questa opzione per una serie di video, per impostare la data di scadenza su 30 giorni rispetto alla data di creazione dei pacchetti.

## Durata caching licenze{#license-caching-duration}

La durata del caching delle licenze specifica per quanto tempo una licenza può essere memorizzata nella cache su disco nell&#39;archivio licenze locale del client senza richiedere la riacquisizione dal server licenze. In alternativa, è possibile specificare una data e un&#39;ora assolute dopo le quali una licenza non può più essere memorizzata nella cache.

Una volta superata la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza al server licenze.

Caso d’uso di esempio: utilizza la durata di memorizzazione nella cache delle licenze per specificare un periodo di tempo fisso valido per una determinata licenza, ad esempio in un caso d’uso di noleggio. Puoi specificare un noleggio di 30 giorni (con inserimento delle licenze nella cache) per indicare la durata totale della licenza entro la quale utilizzare il contenuto.

## Finestra di riproduzione {#playback-window}

La finestra di riproduzione specifica la durata di validità di una licenza dopo il primo utilizzo per la riproduzione di contenuto protetto.

Caso d’uso di esempio: alcuni modelli aziendali consentono un periodo di noleggio di 30 giorni, ma una volta iniziata la riproduzione, questa deve essere completata in 48 ore. In questo caso, la durata di 48 ore della licenza è la finestra di riproduzione.

**Dalla versione 5.3 in poi** - La finestra di riproduzione supporta anche l’opzione di abilitazione o disabilitazione di Hard Stop, che indica se il contesto di decrittografia per la riproduzione deve arrestarsi alla scadenza della finestra di riproduzione (abilitata) o continuare nonostante la scadenza (disabilitata).

>[!NOTE]
>
>L&#39;opzione di arresto rigido non funziona correttamente con la finestra di riproduzione se utilizzata insieme ad essa (la finestra di riproduzione non verrà rispettata). La riproduzione di contenuto con finestra di riproduzione senza interruzione sicura rispetta la restrizione della finestra di riproduzione.
