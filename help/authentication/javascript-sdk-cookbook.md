---
title: Guida di riferimento rapida per l’SDK JavaScript
description: Guida di riferimento rapida per l’SDK JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---


# Guida di riferimento rapida per l’SDK JavaScript {#javascript-sdk-cookbook}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione (#intro)

Questo documento descrive i flussi di lavoro di adesione implementati dall&#39;applicazione di livello superiore di un programmatore per un&#39;integrazione JavaScript con il servizio di autenticazione di Adobe Primetime. I collegamenti al riferimento API JavaScript sono inclusi in tutto.

Tieni presente che [Informazioni correlate](#related) include un collegamento a un set di esempi di codice JavaScript.

## Flussi di adesione (#titlement)

1. [Prerequisiti](#prereq)
2. [Flusso di avvio](#startup)
3. [Flusso di autenticazione](#authn)
4. [Flusso di autorizzazione](#authz)
5. [Visualizza flusso multimediale](#logout)

</br>

![](assets/javascript-flows.png)


## Prerequisiti(#prereq)

**Dipendenze:**

- Libreria di autenticazione Adobe Primetime (AccessEnabler), collabora con il tuo account manager di autenticazione Adobe Primetime per organizzare questo.
- Un requestorId di autenticazione Adobe Primetime valido, collabora con il tuo Account Manager di autenticazione Adobe Primetime per organizzare questo.

Crea le funzioni di callback:

- `entitlementLoaded`

</br>

**Trigger:** L&#39;inizializzazione di AccessEnabler è stata caricata e completata.

- `displayProviderDialog(mvpds)`

   **Trigger:** `getAuthentication(),` solo se l&#39;utente non ha selezionato un provider (un MVPD) e non è ancora autenticato Il parametro mvpds è una matrice di provider disponibili per l&#39;utente.

- `setAuthenticationStatus(status, errorcode)`

   **Trigger:**
   - `checkAuthentication()`ogni volta.
   - `getAuthentication()` solo se l&#39;utente è già autenticato e ha selezionato un provider.

   Lo stato restituito è riuscito o non riuscito; il codice di errore descrive il tipo di errore.

- `createIFrame(width, height)`

   **Trigger:** `setSelectedProvider(providerID)`, solo se il provider selezionato è configurato per essere visualizzato in un IFrame.

   >[!NOTE]
   >
   >Un provider è configurato per eseguire il rendering della schermata di autenticazione come reindirizzamento o in un iFrame e il programmatore deve tenere conto di entrambi.

- `sendTrackingData(event, data)`

   **Triggers:** `checkAuthentication(), getAuthentication(),checkAuthorization(), getAuthorization(), setSelectedProvider()`.  La `event` il parametro indica l&#39;evento di adesione che si è verificato; la `data` è un elenco di valori relativi all&#39;evento. 
- `setToken(token, resource)`

   **Trigger:** `checkAuthorization()`e `getAuthorization()` dopo aver ottenuto l’autorizzazione per visualizzare una risorsa.   La `token` parametro è il token multimediale di breve durata; la `resource` è il contenuto che l&#39;utente è autorizzato a visualizzare.

- `tokenRequestFailed(resource, code, description)`

   **Trigger:**`checkAuthorization()` e`getAuthorization()`  dopo un&#39;autorizzazione non riuscita.\
   La `resource` parametro è il contenuto che l&#39;utente stava tentando di visualizzare; la `code` parametro è il codice di errore che indica il tipo di errore verificatosi; la `description` Il parametro descrive l&#39;errore associato al codice di errore.

- `selectedProvider(mvpd)`

   **Trigger:** [`getSelectedProvider()`](#$getSelProv Il `mvpd` fornisce informazioni sul provider selezionato dall&#39;utente.

- `setMetadataStatus(metadata, key, arguments)`

   **Trigger:** `getMetadata().`\
   La `metadata` fornisce i dati specifici richiesti; il parametro key è la chiave utilizzata nel `getMetadata()`richiesta; e `arguments` è lo stesso dizionario passato a `getMetadata()`.


## 2. Flusso di avvio

**I. Carica il JavaScript di AccessEnabler:**

**Per il profilo di staging**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

o...

**Per profilo di produzione**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

**Triggers:** Al termine dell&#39;inizializzazione, l&#39;autenticazione Adobe Primetime chiama il `entitlementLoaded()` funzione di callback. Questo è il punto di ingresso della comunicazione dell&#39;applicazione con AccessEnabler. 

 
**II.** Chiamata `setRequestor()`stabilire l&#39;identità del programmatore; trasmettere il `requestorID` e (facoltativamente) un array di endpoint di autenticazione Adobe Primetime.

**Triggers:** Nessuno, ma abilita `displayProviderDialog()` da chiamare quando necessario.


**III.** Chiamata `checkAuthentication()` per verificare la presenza di un&#39;autenticazione esistente senza avviare l&#39;intero processo [flusso di autenticazione].  Se questa chiamata ha esito positivo, puoi procedere direttamente alla `authorization flow`.  In caso contrario, procedere alla `authentication flow`.

**Dipendenza:** Chiamata riuscita a `setRequestor()`(questa dipendenza si applica anche a tutte le chiamate successive).

 **Triggers:** `setAuthenticationStatus()` callback

</br>

## 3. Flusso di autenticazione</span>


**Dipendenza:** Chiamata riuscita a `setRequestor()`(questa dipendenza si applica anche a tutte le chiamate successive).


Chiamata `getAuthentication()` per ottenere lo stato di autenticazione O per attivare il flusso di autenticazione del provider.

**Attivatori:**

- `displayProviderDialog()`se l&#39;utente non è ancora stato autenticato
- `setAuthenticationStatus()` se l&#39;autenticazione è già avvenuta

Il completamento del flusso di autenticazione viene raggiunto quando AccessEnabler chiama `setAuthenticationStatus()`con `isAuthenticated == 1`.

## 4. Flusso di autorizzazione (#authz)

**Dipendenze:**

- Chiamata riuscita a `setRequestor()` (questa dipendenza si applica anche a tutte le chiamate successive).
- ResourceID(s) valido(i) concordato con l&#39;MVPD(s). Gli ID risorsa devono essere gli stessi utilizzati su qualsiasi altro dispositivo o piattaforma e devono essere gli stessi in tutti gli MVPD.

Chiamata `getAuthorization()` e passare il ResourceID per il supporto richiesto. Una chiamata corretta restituirà un token per contenuti multimediali brevi, che conferma che l’utente è autorizzato a visualizzare i file multimediali richiesti.

- Se la chiamata passa: L&#39;utente dispone di un token AuthN valido e l&#39;utente è autorizzato a guardare il supporto richiesto.
- Se la chiamata non riesce: Esamina l’eccezione generata per determinare il relativo tipo (AuthN, AuthZ o altro):
- Se la chiamata era un errore AuthN, riavvia il flusso AuthN.
- Se la chiamata è stata un errore AuthZ, l’utente non è autorizzato a guardare il supporto richiesto e deve essere visualizzato un messaggio di errore di qualche tipo.
- Se si è verificato un altro errore (errore di connessione, errore di rete, ecc.) quindi mostrare all’utente un messaggio di errore appropriato.

Utilizza il Media Token Verifier per convalidare il shortMediaToken restituito da un `getAuthorization()` chiama.

 
**Dipendenza:** Il verificatore di token per contenuti multimediali brevi (incluso nella libreria AccessEnabler)

- Se la convalida viene superata: Visualizza/riproduce il supporto richiesto per l&#39;utente.
- In caso di errore: Il token AuthZ non è valido. La richiesta multimediale deve essere rifiutata e deve essere visualizzato un messaggio di errore all&#39;utente.

## 5. Visualizza flusso multimediale (#logout)

- L&#39;utente seleziona il supporto da visualizzare.
   - I supporti sono protetti?\
          - L&#39;app controlla se il contenuto multimediale è protetto:
      - Se il contenuto multimediale è protetto, l’app avvia il flusso di autorizzazione (AuthZ) riportato sopra.
      - Se il supporto non è protetto, procedere con il flusso Visualizza file multimediali.
      - Supporti di riproduzione

## Configurazione dell’ID visitatore (#visitorID)

Configurazione di un [Experience Cloud visitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) dal punto di vista dell’analisi, il valore è molto importante. Una volta impostato il valore visitorID EC, l&#39;SDK invierà queste informazioni insieme a ogni chiamata di rete e il servizio di autenticazione Adobe Primetime raccoglierà queste informazioni. In questo modo potrai correlare i dati di analisi del servizio di autenticazione di Adobe Primetime con qualsiasi altro rapporto di analisi disponibile da altre applicazioni o siti web. Informazioni su come impostare EC visitorID sono disponibili [qui](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=en).

 
>[!NOTE]
>
>Questo supporto funzionalità è disponibile a partire dalla versione 3.1.0 dell’SDK JS. 

<!--
### Related Information (#related)

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
* **JavaScript SDK Code Samples**
-->