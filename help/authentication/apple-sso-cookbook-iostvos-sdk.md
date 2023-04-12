---
title: Cookie Apple SSO (iOS/tvOS SDK)
description: Cookie Apple SSO (iOS/tvOS SDK)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 0%

---



# Cookie Apple SSO (iOS/tvOS SDK) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#Introduction}

L&#39;SDK di Adobe Primetime Authentication AccessEnabler iOS/tvOS può supportare l&#39;autenticazione Single Sign-On (SSO) della piattaforma per gli utenti finali delle applicazioni client in esecuzione su iOS, iPadOS o tvOS attraverso quello che chiamiamo flusso di lavoro SSO di Apple.

Nota che questo documento funge da estensione della documentazione esistente dell&#39;SDK iOS/tvOS di AccessEnabler, che si trova [qui](/help/authentication/iostvos-sdk-api-reference.md).

</br>

## Guida di riferimento {#Cookbook}

Per poter beneficiare dell’esperienza utente Apple SSO, un’applicazione deve integrare l’SDK di AccessEnabler iOS/tvOS e seguire la sequenza di suggerimenti riportati di seguito.

</br>

### Prerequisiti {#Prerequisites}

</br>

#### Autorizzazione

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Per poter accedere alle informazioni di abbonamento dell&#39;utente, l&#39;utente deve concedere all&#39;applicazione l&#39;autorizzazione a procedere, in modo analogo all&#39;accesso alla fotocamera o al microfono del dispositivo. Questa autorizzazione deve essere richiesta per applicazione e il dispositivo salverà la selezione dell&#39;utente. Tenere presente che l&#39;utente può cambiare la propria decisione andando alle impostazioni dell&#39;applicazione (accesso all&#39;autorizzazione del fornitore TV) o alla sezione da *`Settings -> TV Provider`* su iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* su tvOS.

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** È consigliabile richiedere l’autorizzazione dell’utente quando l’applicazione entra in primo piano, ma si tratta solo di un suggerimento, perché l’applicazione può verificare la presenza di [autorizzazione di accesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) le informazioni di abbonamento dell’utente in qualsiasi momento prima di richiedere l’autenticazione dell’utente. Inoltre, le API SDK di AccessEnabler iOS/tvOS richiederanno automaticamente l&#39;autorizzazione dell&#39;utente quando ne ha bisogno.

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Se l’utente non concede l’accesso alle informazioni di abbonamento o se la comunicazione con il framework dell’account del sottoscrittore video non riesce, l’SDK di AccessEnabler iOS/tvOS si basa sul flusso di autenticazione regolare.

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Si consiglia di incentivare gli utenti che si rifiutano di concedere l’autorizzazione all’accesso alle informazioni di abbonamento spiegando i vantaggi dell’esperienza utente Single Sign-On (SSO). Tenere presente che l&#39;utente può cambiare la propria decisione andando alle impostazioni dell&#39;applicazione (accesso all&#39;autorizzazione del fornitore TV) o alla sezione da *`Settings -> TV Provider`* su iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* su tvOS.


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                   // Do nothing.
                
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                   // Incentivize users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from Settings -> TV Provider on iOS/iPadOS or Settings -> Accounts -> TV Provider on tvOS.
                   ...
                }
    }
    ... 
```

</br>

#### Callback

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Implementa il seguente elenco di [callback](/help/authentication/iostvos-sdk-api-reference.md) che sono specifici del flusso di lavoro SSO di Apple.

- [*presentTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog) - Callback attivato quando si aprirà il selettore MVPD di Apple.
- [*dismissTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog) - Callback attivato quando il selettore MVPD di Apple sta per chiudersi.

</br>

#### Segnalazione errori

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Implementa il seguente elenco di [codici di errore avanzati](/help/authentication/error-reporting.md) che sono specifiche del flusso di lavoro SSO di Apple.

- ***N003*** - L&#39;utente ha selezionato l&#39;opzione &quot;Altro fornitore TV&quot; dal selettore MVPD di Apple.
- ***N004*** - L&#39;utente ha selezionato un provider TV dal selettore MVPD di Apple, che non è supportato (integrazione o Single Sign-On disabilitata) dal richiedente corrente.
- ***N005*** - L&#39;utente ha deciso di annullare il selettore MVPD regolare o il selettore MVPD Apple.
- ***VSA403*** - L&#39;autorizzazione del provider TV dell&#39;utente è negata per l&#39;applicazione.
- ***VSA404*** - L&#39;autorizzazione del provider TV dell&#39;utente è indeterminata per l&#39;applicazione.
- ***VSA503*** - Richiesta dei metadati dell&#39;account del sottoscrittore video non riuscita. Viene fornito più contesto in *message* campo .
- ***AAPL / APPL_ERROR*** - Richiesta dei metadati dell&#39;account del sottoscrittore video non riuscita. Viene fornito più contesto in *dettagli* campo . 

</br>

### Autenticazione {#Authentication}

>[!TIP]
>
> **<u>Suggerimento:</u>** Segui i passaggi riportati di seguito per l&#39;implementazione/i di iOS/iPadOS/tvOS.

1. La domanda deve [initialize](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) SDK di AccessEnabler per iOS/tvOS.
1. La domanda deve [imposta l&#39;identificatore del richiedente corrente](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

   **Importante:** Questo secondo passaggio potrebbe attivare un [codice di errore avanzato](/help/authentication/error-reporting.md) specifico per il flusso di lavoro SSO Apple, nel caso **una delle seguenti affermazioni è vera**:

   - ***VSA403*** - L&#39;autorizzazione del provider TV dell&#39;utente è negata per l&#39;applicazione.
   - ***VSA404*** - L&#39;autorizzazione del provider TV dell&#39;utente è indeterminata per l&#39;applicazione.
   - ***APPL*** - La comunicazione tra l&#39;SDK iOS/tvOS di AccessEnabler e il framework dell&#39;account utente con sottoscrizione video ha rilevato un errore.

   Questo secondo passaggio cerca di scambiare silenziosamente il profilo SSO Apple per un token di autenticazione Adobe, nel caso in cui **tutti i precedenti sono falsi** e **tutte le seguenti affermazioni sono vere**:

   - L&#39;autorizzazione del provider TV dell&#39;utente è concessa per l&#39;applicazione.
   - L&#39;utente ha effettuato l&#39;accesso al proprio account TV Provider a livello di sistema del dispositivo.
   - L&#39;SDK di AccessEnabler iOS/tvOS ha ricevuto l&#39;identificatore del provider TV dell&#39;utente dal framework dell&#39;account del sottoscrittore video.
   - L’integrazione dell’utente con il provider TV con l’applicazione viene abilitata tramite la dashboard TVE di Adobe Primetime.
   - Il Single Sign-On del provider TV dell&#39;utente con l&#39;applicazione è abilitato tramite la dashboard TVE di Adobe Primetime.
   - Il provider TV dell&#39;utente non viene danneggiato dal dashboard TVE di Adobe Primetime.
   - L&#39;SDK iOS/tvOS di AccessEnabler ha ricevuto la risposta SAML del provider TV dell&#39;utente dal framework dell&#39;account utente sottoscrittore video.

   **<u>Suggerimento Pro:</u>** Questo secondo passaggio non attiverà nessun altro callback, oltre al [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) callback, poiché l&#39;autenticazione non è stata avviata in modo esplicito dall&#39;applicazione.

1. La domanda deve [controlla lo stato di autenticazione](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

   **Importante:** Questo terzo passaggio potrebbe attivare un [codice di errore avanzato](/help/authentication/error-reporting.md) specifico per il flusso di lavoro SSO Apple, nel caso **una delle seguenti affermazioni è vera**:

   - ***VSA403** - L&#39;utente ha effettuato l&#39;accesso al proprio account TV Provider a livello di sistema del dispositivo, ma l&#39;autorizzazione TV Provider dell&#39;utente è negata per l&#39;applicazione.
   - ***VSA404** - L&#39;utente ha effettuato l&#39;accesso al proprio account TV Provider a livello di sistema del dispositivo, ma l&#39;autorizzazione TV Provider dell&#39;utente è indeterminata per l&#39;applicazione.
   - ***APPL\_ERROR** - L&#39;utente ha effettuato l&#39;accesso al proprio account del provider TV a livello di sistema del dispositivo, ma la comunicazione tra l&#39;SDK di AccessEnabler iOS/tvOS e il framework dell&#39;account del sottoscrittore video ha rilevato un errore.

   **Importante:** Questo terzo passaggio attiverà la [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback con *status* uguale a 0, nel caso **una delle seguenti affermazioni è vera**:

   - L&#39;utente non ha effettuato l&#39;accesso al proprio account del provider TV a livello di sistema del dispositivo o tramite un flusso di autenticazione regolare.
   - L&#39;utente ha effettuato l&#39;accesso al proprio account del provider TV a livello di sistema del dispositivo o tramite un flusso di autenticazione regolare, ma il token di autenticazione del provider TV dell&#39;utente TTL è passato.
   - L&#39;utente ha effettuato l&#39;accesso al proprio account del provider TV a livello di sistema del dispositivo o tramite un flusso di autenticazione regolare, ma l&#39;integrazione del provider TV dell&#39;utente con l&#39;applicazione viene disabilitata tramite il dashboard TVE di Adobe Primetime.
   - L&#39;utente ha effettuato l&#39;accesso al proprio account del provider TV a livello di sistema del dispositivo, ma il Single Sign-On del provider TV con l&#39;applicazione è disabilitato tramite il dashboard TVE di Adobe Primetime.
   - L&#39;utente ha effettuato l&#39;accesso al proprio account TV Provider a livello di sistema del dispositivo, ma l&#39;autorizzazione TV Provider dell&#39;utente è negata per l&#39;applicazione.
   - L&#39;utente ha effettuato l&#39;accesso al proprio account TV Provider a livello di sistema del dispositivo, ma l&#39;autorizzazione TV Provider dell&#39;utente è indeterminata per l&#39;applicazione.
   - L&#39;utente ha effettuato l&#39;accesso al proprio account del provider TV a livello di sistema del dispositivo, ma la comunicazione tra l&#39;SDK di AccessEnabler iOS/tvOS e il framework dell&#39;account del sottoscrittore video ha rilevato un errore.

   **Importante:** Questo terzo passaggio attiverà la [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback con *status* uguale a 1, nel caso **tutti i precedenti sono falsi.**


1. La domanda deve [inizializza l&#39;autenticazione](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) nel caso in cui il precedente controllo dello stato di autenticazione attivasse il [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback con *status* uguale a 0.

   **<u>Suggerimento Pro:</u>** Implementa una delle seguenti API SDK di AccessEnabler per iOS/tvOS [getAuthentication](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) o [getAuthentication:filter](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter).

   **Importante:** Questo quarto passaggio potrebbe innescare un [codice di errore avanzato](/help/authentication/error-reporting.md) specifico per il flusso di lavoro SSO Apple, nel caso **una delle seguenti affermazioni è vera**:

   - ***VSA403*** - L&#39;autorizzazione del provider TV dell&#39;utente è negata per l&#39;applicazione.
   - ***VSA404*** - L&#39;autorizzazione del provider TV dell&#39;utente è indeterminata per l&#39;applicazione.
   - ***VSA503*** - La comunicazione tra l&#39;SDK iOS/tvOS di AccessEnabler e il framework dell&#39;account utente con sottoscrizione video ha rilevato un errore.
   - ***N003*** - L&#39;utente ha selezionato l&#39;opzione &quot;Altro fornitore TV&quot; dal selettore MVPD di Apple.
   - ***N004*** - L&#39;utente ha selezionato un provider TV dal selettore MVPD di Apple, che non è supportato (integrazione o Single Sign-On disabilitata) dal richiedente corrente.
   - ***N005*** - L&#39;utente ha deciso di annullare il selettore MVPD regolare o il selettore MVPD Apple.

   **Importante:** Questo quarto passaggio si basa sul normale flusso di autenticazione, attivando il [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) callback e **uno** di cui sopra [codici di errore avanzati](/help/authentication/error-reporting.md), nel caso **una delle affermazioni di cui sopra è vera**. 

   **Importante:** Questo quarto passaggio si basa sul normale flusso di autenticazione, attivando il [navigaToUrl](/help/authentication/iostvos-sdk-api-reference.md#nav2url) o [navigaToUrl:useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) callback e **nessuno** di cui sopra [codici di errore avanzati](/help/authentication/error-reporting.md), nel caso in cui l&#39;utente abbia selezionato un provider TV che non supporta Apple SSO, ma è presente nel selettore MVPD di Apple.

   **<u>Suggerimento Pro:</u>** L&#39;SDK di AccessEnabler iOS/tvOS chiama silenziosamente il [setSelectedProvider](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) API, nel caso in cui l&#39;utente abbia selezionato un provider TV, che non supporta Apple SSO, ma è presente nel selettore MVPD di Apple.

   **Importante:** Questo quarto passaggio cercherebbe di scambiare silenziosamente il profilo SSO di Apple per un token di autenticazione Adobe, nel caso in cui **tutti i precedenti sono falsi** e **tutte le seguenti affermazioni sono vere**:

   - L&#39;autorizzazione del provider TV dell&#39;utente è concessa per l&#39;applicazione.
   - L&#39;utente ha effettuato l&#39;accesso / attualmente accede al suo account del fornitore TV a livello di sistema del dispositivo.
   - L&#39;SDK di AccessEnabler iOS/tvOS ha ricevuto l&#39;identificatore del provider TV dell&#39;utente dal framework dell&#39;account del sottoscrittore video.
   - L’integrazione dell’utente con il provider TV con l’applicazione viene abilitata tramite la dashboard TVE di Adobe Primetime.
   - Il Single Sign-On del provider TV dell&#39;utente con l&#39;applicazione è abilitato tramite la dashboard TVE di Adobe Primetime.
   - Il provider TV dell&#39;utente non viene danneggiato dal dashboard TVE di Adobe Primetime.
   - L&#39;SDK iOS/tvOS di AccessEnabler ha ricevuto la risposta SAML del provider TV dell&#39;utente dal framework dell&#39;account utente sottoscrittore video.


 

>**<u>Suggerimento Pro:</u>** Questo quarto passaggio attiverà la [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) callback, indipendentemente *status* risultato, poiché l&#39;autenticazione è stata avviata esplicitamente dall&#39;applicazione.


</br>

### Metadati {#Metadata}

L&#39;applicazione ha la possibilità di determinare se l&#39;autenticazione è avvenuta in seguito a un accesso tramite la piattaforma SSO o meno, utilizzando &quot;*tokenSource&quot;* [metadati utente](/help/authentication/iostvos-sdk-api-reference.md#getMeta) API da AccessEnabler iOS/tvOS SDK.

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### Logout {#Logout}

La [Account utente con sottoscrizione video](https://developer.apple.com/documentation/videosubscriberaccount) framework non fornisce un&#39;API per disconnettersi programmaticamente le persone che hanno effettuato l&#39;accesso al proprio account del provider TV a livello di sistema del dispositivo. Pertanto, affinché l’logout abbia effetto completo, l’utente finale dovrà esplicitamente disconnettersi da *`Settings -> TV Provider`* su iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* su tvOS. L&#39;altra opzione che l&#39;utente dovrebbe avere è quella di revocare il permesso di accedere alle informazioni di abbonamento dell&#39;utente dalla sezione specifica impostazioni dell&#39;applicazione (accesso al permesso del fornitore TV).

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite l’SDK iOS/tvOS di AccessEnabler [disconnessione](/help/authentication/iostvos-sdk-api-reference.md#logout) API.


>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Segui i passaggi riportati di seguito per l&#39;implementazione o le implementazioni tvOS.

- La domanda deve [avvia il logout](/help/authentication/iostvos-sdk-api-reference.md#logout) dall&#39;SDK iOS/tvOS di AccessEnabler. Questo non faciliterebbe la pulizia delle sessioni sul lato MVPD.
- L&#39;applicazione deve istruire/richiedere all&#39;utente di disconnettersi in modo esplicito da *`Settings -> Accounts -> TV Provider`* solo su tvOS nel caso [*VSA203* il codice di stato viene attivato](/help/authentication/error-reporting.md).

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Segui i passaggi riportati di seguito per l’implementazione di iOS/iPadOS.

- La domanda deve [avvia il logout](/help/authentication/iostvos-sdk-api-reference.md#logout) dall&#39;SDK iOS/tvOS di AccessEnabler. Questo faciliterebbe la pulizia delle sessioni sul lato MVPD.
- L&#39;applicazione deve istruire/richiedere all&#39;utente di disconnettersi in modo esplicito da *`Settings -> TV Provider`* solo su iOS/iPadOS nel caso [*VSA203* il codice di stato viene attivato](/help/authentication/error-reporting.md).


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
