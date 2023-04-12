---
title: Integrazione dei dati lato server di autenticazione Primetime in Adobe Analytics
description: Integrazione dei dati lato server di autenticazione Primetime in Adobe Analytics
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 4%

---


# Integrazione dei dati lato server di Primetime Authentication in Adobe Analytics

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

I clienti di Adobe Primetime Authentication desiderano visualizzare i dati lato server di Primetime Authentication (Adobe Pass) nella dashboard di Adobe Analytics per un consumo più semplice.

I dati serviranno a monitorare importanti metriche TVE come i tassi di conversione dell’autenticazione per MVPD, gli utenti univoci basati sull’ID utente MVPD e altro ancora.

Non è destinato a sostituire un’implementazione lato client se già esistente, poiché l’attività utente non può essere tracciata oltre gli eventi specifici riportati di seguito in assenza di un ID visitatore. Se i clienti forniscono un ID visitatore per le chiamate Pass , possiamo sbloccare un altro tipo di integrazione Analytics - in tempo reale - che può unire tutti gli eventi Pass con i dati dei clienti esistenti. Maggiori dettagli su questo nuovo tipo di integrazione possibile qui: &quot;[Utilizzo dell&#39;ID di Experience Cloud nell&#39;autenticazione di Primetime](/help/authentication/exp-cloud-id-authn.md)&quot;

## Metriche incluse {#metrics-included-int-authn-analyt}

| Evento | Descrizione |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| AuthN richiesto | Numero di flussi di autenticazione avviati |
| AuthN in sospeso | Numero di token di autenticazione generati correttamente (senza tenere conto del fatto che il client lo abbia effettivamente ottenuto) |
| AuthN OK | Numero di token di autenticazione ottenuti correttamente dagli utenti |
| AuthZ richiesto | Numero di autorizzazioni tentate |
| AuthZ OK | Numero di autorizzazioni riuscite |
| AuthZ non riuscita | Numero di autorizzazioni negate da MVPD a livello di applicazione |
| Richiesta di riproduzione | Numero di token multimediali brevi generati (che si assimilano al numero di richieste di riproduzione) |
| Logout richiesto | Numero di flussi di logout avviati |
| Disconnessione completata | Numero di flussi di logout completati con successo |
| Disconnessione non riuscita | Numero di flussi di logout non riusciti |
| Preautorizzazione richiesta | Numero di flussi di preautorizzazione avviati |
| Autorizzazione OK | Numero di eventi di preautorizzazione riusciti con le risorse preautorizzate |
| Autorizzazione negata | Numero di eventi di preautorizzazione con le risorse a cui è stata negata la preautorizzazione |
| Preautorizzazione non riuscita | Numero di eventi di preautorizzazione non riusciti |

| Nome Adobe Analytics | Descrizione |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Canale | ID richiedente utilizzato per eseguire la richiesta di adesione |
| MVPD | MVPD responsabile della concessione del diritto all&#39;utente |
| Proxy | Il proxy MVPD (che sarà &quot;Diretto&quot; per le integrazioni dirette) |
| Tipo SDK | L’SDK client utilizzato (Flash, HTML5, nativo Android, iOS, Clientless, ecc.) |
| Versione SDK | Versione dell’SDK del client di autenticazione Adobe Primetime |
| ID risorsa | Titolo della risorsa effettiva coinvolta nella richiesta di autorizzazione (estratto dal payload MRSS come elemento/titolo, se fornito) |
| Tipo di errore AuthZ | Motivo degli errori, come segnalato dall’autenticazione Adobe Primetime <br/> Di seguito sono riportati i valori più comuni <br/> **noAuthZ** = l&#39;MVPD risponde che l&#39;utente non ha il canale nel suo pacchetto<br/> **rete** = non siamo riusciti a raggiungere l&#39;MVPD (MVPD ha un problema al momento della chiamata e non ha risposto)<br/> **norefreshtoken** = questo è strettamente per le implementazioni OAuth e potrebbe comportare la modifica della password da parte dell’utente o la negazione da parte dell’MVPD per qualche motivo. Generalmente si traduce in una nuova autenticazione<br/> **disallineamento** = se la richiesta viene effettuata da un dispositivo diverso da quello con il token di autenticazione. Può comportare se gli utenti tentano di ingannare il sistema, ma la maggior parte di questi è avvenuta nel contesto del nostro vecchio SDK JavaScript in cui l&#39;ID dispositivo stava utilizzando l&#39;indirizzo IP come parte del calcolo. Se un utente guardava TVE a casa e poi sul posto di lavoro, questo errore veniva attivato e doveva nuovamente eseguire l&#39;autenticazione.<br/> **non valido** = richiesta non valida, parametri mancanti o non validi<br/>  **authzNone** = I programmatori hanno la possibilità di negare le autorizzazioni per una specifica combinazione di cannelxMVPD. Questo viene attivato da un’API back-end a cui i programmatori hanno accesso<br/> **frode** = è un meccanismo di protezione dalla nostra parte. Se l’utente non ottiene l’autorizzazione e quindi la richiede di nuovo un numero di volte in un breve intervallo (secondi), neghiamo la chiamata direttamente. Generalmente accade quando un programmatore ha un bug nella sua implementazione che richiede costantemente l&#39;autorizzazione se non riesce. |
| Tipo di token | Quando i token vengono creati a causa di AuthZ All e AuthN All, dobbiamo sapere cosa sono prodotti a causa di una misura di degradazione.<br/> Sono:<br/> &quot;Normal&quot; = il caso normale<br/> &quot;authnall&quot; = Quando AuthN All è abilitato<br/> &quot;authzall&quot; = Quando AuthZ All è abilitato<br/>  &quot;hba&quot; = Quando l&#39;HBA è abilitato |
| Tipo di dispositivo senza client | La piattaforma dispositivo (alternativa), attualmente utilizzata per Clientless.<br/> I valori possono essere:<br/> N/D: l’evento non è nato da un SDK Clientless<br/> Sconosciuto - Dal parametro deviceType da un **API senza client** è facoltativo; sono presenti chiamate che non contengono alcun valore.<br/> Qualsiasi altro valore inviato tramite **API senza client**. Ad esempio, xbox, appletv e roku. |
| ID utente MVPD | Sostituisce l&#39;ID visitatore basato su cookie |


## Dettagli {#details-int-authn-analyt}

* Le metriche verranno inserite, evento per evento nella suite di rapporti specifica tramite l’API di inserimento dati di Adobe Analytics
* L&#39;inserimento verrà batch e inviato ogni 30 minuti. Per questo motivo, il rapporto deve avere un timestamp
* Ogni cliente avrà una o più suite di rapporti. Un ID richiedente (canale) verrà mappato su una sola suite di rapporti. Più requestor ID possono essere mappati su una sola suite di rapporti.
* I dati storici possono essere forniti, ma occorre prestare particolare attenzione a causa di problemi di traffico/prestazioni.
* La variabile visitatore univoco è impostata sull’ID utente MVPD
* La mappatura di eventi ed eVar non è configurabile.


## SLA {#sla-int-authn-serv-anal}

Poiché non si tratta di un componente critico, non esiste alcuna garanzia SLA per l&#39;integrazione.

## Configurazione della suite di rapporti {#report-suite-config}

Il rapporto deve essere contrassegnato da una marca temporale poiché gli eventi vengono inviati in batch.

### Eventi {#report-suite-config-events}


>[!NOTE]
>Tutto deve essere impostato con:
>
>* Contatore (nessuna sub-relazione)


| Evento | Evento Adobe Analytics |
|---------------------------------------|-----------------------|
| AuthN richiesto | event1 |
| AuthN in sospeso | event2 |
| AuthN OK | event3 |
| AuthZ richiesto | event4 |
| AuthZ OK | event5 |
| AuthZ non riuscita | event6 |
| Richiesta di riproduzione | event7 |
| AuthN non riuscito | event8 |
| Richiesta token AuthN senza client OK | event9 |
| Richiesta token AuthN senza client non riuscita | event10 |
| Richiesta di riproduzione non riuscita | event11 |
| Richiesta di disconnessione | event12 |
| Disconnessione completata | event13 |
| Disconnessione non riuscita | event14 |
| Richiesta di verifica preliminare | event15 |
| Preflight non riuscito | event16 |
| Preflight concesso | event17 |
| Preflight negato | event18 |


### eVar {#evars}


>[!NOTE]
>Tutto deve essere impostato con:
>
>* Allocazione: Più recente (ultimo)
>* Scade dopo: Hit
>* Tipo: Stringa di testo


| Proprietà | eVar |
|-----------------------------------|--------------------------------|
| Canale | eVar1 |
| MVPD | eVar2 |
| Proxy | eVar3 |
| Tipo SDK | eVar4 |
| Versione SDK | eVar5 |
| ID risorsa | eVar6 |
| Tipo di errore AuthZ | eVar7 |
| Tipo di token | eVar8 |
| Tipo di dispositivo senza client | eVar9 |
| ID utente MVPD | visitorID (eseguito automaticamente) |
| ID utente MVPD | eVar10 |
| Tipo di dispositivo | eVar11 |
| Sistema operativo | eVar12 |
| Tipo di hardware principale | eVar13 |
| TTL | eVar14 |
| Tipo di autenticazione | eVar15 |
| Versione dell&#39;architettura del server | eVar16 |
| Provider di autenticazione esterno | eVar17 |
| Latenza | eVar18 |
| ID visitatore | eVar19 |
| Meccanismo SSO | eVar20 |
| Modello dispositivo | eVar21 |
| Versione dispositivo | eVar22 |
| Modello hardware del dispositivo | eVar23 |
| Fornitore hardware del dispositivo | eVar24 |
| Produttore hardware del dispositivo | eVar25 |
| Versione hardware del dispositivo | eVar26 |
| Nome del sistema operativo del dispositivo | eVar27 |
| Famiglia di dispositivi operativi | eVar28 |
| Fornitore sistema operativo del dispositivo | eVar29 |
| Versione sistema operativo del dispositivo | eVar30 |
| Nome del browser del dispositivo | eVar31 |
| Fornitore browser del dispositivo | eVar32 |
| Versione browser del dispositivo | eVar33 |
| Tipo di dispositivo senza client normalizzato | eVar34 |

## Prezzi {#pricing}

Contatta il tuo TAM per maggiori informazioni.
