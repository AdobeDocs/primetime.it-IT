---
title: Panoramica di Apple SSO
description: Panoramica di Apple SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---



# Panoramica di Apple SSO {#apple-sso-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#Introduction}

Apple fornisce un’API che consente alle persone di accedere al proprio account del provider TV a livello di sistema del dispositivo, eliminando la necessità di eseguire l’autenticazione in base all’app.

Di conseguenza, Apple e Adobe Primetime Authentication hanno collaborato per creare l&#39;esperienza utente della piattaforma Single Sign-On (SSO) nell&#39;ecosistema TV Everywhere per i proprietari di iPhone, iPad e Apple TV.

Per beneficiare dell’esperienza utente Single Sign-On (SSO) su un dispositivo Apple, è necessario completare un elenco di prerequisiti.

</br>

## Prerequisiti {#Prerequisites}

I prerequisiti possono essere applicati a una o più entità coinvolte nel business TVE, come programmatori, MVPD, autenticazione Adobe Primetime o Apple.

</br>

### Programmatore {#Programmer}

Per poter beneficiare dell&#39;esperienza utente Single Sign-On (SSO), un programmatore deve:

1. Utilizza almeno la versione 8 di Xcode e iOS/tvOS versione 10.

1. Avere [Autorizzazione Single Sign-On per sottoscrittori video](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) configurato per il proprio account sviluppatore Apple. Contatta Apple per abilitare [Framework account utente con sottoscrizione video](https://developer.apple.com/documentation/videosubscriberaccount) per il tuo ID team Apple.

1. Abilita Single Sign-On (YES) per ogni integrazione desiderata (Channel x MVPD) e la piattaforma desiderata (iOS / tvOS) tramite [Dashboard TVE di Adobe Primetime](https://console.auth.adobe.com/).

1. Integra i flussi di lavoro Apple SSO utilizzando una delle due soluzioni seguenti offerte dal team di autenticazione di Adobe Primetime:

   - L&#39;API REST di autenticazione Adobe Primetime può supportare l&#39;autenticazione Single Sign-On (SSO) della piattaforma per gli utenti finali di applicazioni client in esecuzione su iOS, iPadOS o tvOS. Vedi anche [Cookie Apple SSO (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md).

   - L&#39;SDK di Adobe Primetime Authentication AccessEnabler iOS/tvOS può supportare l&#39;autenticazione Single Sign-On (SSO) della piattaforma per gli utenti finali delle applicazioni client in esecuzione su iOS, iPadOS o tvOS. Vedi anche [Cookie Apple SSO (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

   - **<u>Suggerimento Pro:</u>** Per poter accedere alle informazioni di abbonamento dell&#39;utente, l&#39;utente deve concedere all&#39;applicazione l&#39;autorizzazione a procedere, in modo analogo all&#39;accesso alla fotocamera o al microfono del dispositivo. Questa autorizzazione deve essere richiesta per applicazione e il dispositivo salverà la selezione dell&#39;utente. Tenere presente che l&#39;utente può cambiare la propria decisione andando alle impostazioni dell&#39;applicazione (accesso all&#39;autorizzazione del fornitore TV) o alla sezione da *`Settings -> TV Provider`* su iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* su tvOS.

   - **<u>Suggerimento Pro:</u>** È consigliabile richiedere l’autorizzazione dell’utente quando l’applicazione entra in primo piano, ma si tratta solo di un suggerimento, perché l’applicazione può verificare la presenza di [autorizzazione di accesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) le informazioni di abbonamento dell’utente in qualsiasi momento prima di richiedere l’autenticazione dell’utente. Inoltre, le API SDK di AccessEnabler iOS/tvOS richiederanno automaticamente l&#39;autorizzazione dell&#39;utente quando ne ha bisogno.

   - **<u>Suggerimento Pro:</u>** Si consiglia di incentivare gli utenti che si rifiutano di concedere l’autorizzazione all’accesso alle informazioni di abbonamento spiegando i vantaggi dell’esperienza utente Single Sign-On (SSO). Tenere presente che l&#39;utente può cambiare la propria decisione andando alle impostazioni dell&#39;applicazione (accesso all&#39;autorizzazione del fornitore TV) o alla sezione da *`Settings -> TV Provider`* su iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* su tvOS.

Il risultato dovrebbe creare un’esperienza in linea con i seguenti flussi di utenti, che consigliamo di consultare prima di iniziare a sviluppare le applicazioni:

- [iPhone / iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) flussi utente
- [Apple TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) flussi utente


>[!IMPORTANT]
>
> Quando la funzione Single Sign-On è **abilitato** per iOS/tvOS **e** nel caso di Apple **onboarded (supportato) o picker** MVPD i flussi di autenticazione/logout dai flussi di lavoro SSO di Apple coinvolgeranno sia le soluzioni di autenticazione di Apple che Adobe Primetime, mentre tutti gli altri flussi (autorizzazione, preautorizzazione, metadati, ecc.) saranno serviti solo da Adobe Primetime Authentication.


>[!IMPORTANT]
>
> Quando la funzione Single Sign-On è **disattivato** per iOS/tvOS **o** nel caso di Apple **non integrato (non supportato)** MVPDs i flussi di autenticazione/logout ricadranno dai flussi di lavoro Apple SSO a quelli regolari gestiti esclusivamente dall’autenticazione Adobe Primetime.


>[!IMPORTANT]
>
> Un guadagno principale del flusso di lavoro Apple SSO è rappresentato dal flusso utente di autenticazione a schermo singolo, che può essere distribuito anche su Apple TV quando la funzione Single Sign-On è **abilitato** per tvOS **e** nel caso di Apple **onboarded (supportato)** MVPD.


### MVPD {#MVPD}

Per poter beneficiare dell’esperienza utente Single Sign-On (SSO), un MVPD deve:

 

1. Accedi al flusso di lavoro SSO di Apple sul lato Apple. Contatta Apple per facilitare il processo di onboarding.
1. Fornire un&#39;applicazione JavaScript TVML in grado di gestire il modulo di accesso utente. Contatta Apple per ricevere la documentazione appropriata.
1. Specifica un valore stringa che rappresenta l&#39;identificatore del provider assegnato da Apple durante il processo di onboarding. Contatta l’autenticazione Adobe Primetime per eseguire le modifiche alla configurazione.

</br>

## Domande frequenti {#FAQ}

1. Nel caso in cui si verifichi un problema con il flusso di lavoro Apple SSO, l&#39;applicazione che utilizza l&#39;SDK di AccessEnabler iOS/tvOS può fare riferimento al flusso di autenticazione regolare?
   - Ciò è possibile ma richiede l’esecuzione di una modifica della configurazione sul [Dashboard TVE di Adobe Primetime](https://console.auth.adobe.com/). La *Abilita Single Sign-On* deve essere impostato su *NO* per l&#39;integrazione desiderata (Channel x MVPD) e la piattaforma desiderata (iOS/tvOS).
   - L&#39;applicazione riconosce la modifica della configurazione solo dopo aver chiamato [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) API nel caso in cui utilizzi AccessEnabler iOS/tvOS SDK.
1. L&#39;applicazione saprà quando è avvenuta un&#39;autenticazione a seguito di un accesso tramite la piattaforma SSO su un altro dispositivo o un&#39;altra applicazione?
   - Queste informazioni non saranno disponibili.
1. L&#39;applicazione saprà quando è avvenuta un&#39;autenticazione a seguito di un accesso tramite la piattaforma SSO sullo stesso dispositivo? 
   - Queste informazioni sono disponibili come parte della chiave di metadati utente: *tokenSource*, che deve restituire il valore della stringa: &quot;Apple&quot; in questo caso.
1. Cosa succede se un utente effettua l’accesso andando al *`Settings -> TV Provider`* su iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* nella sezione tvOS utilizzando un MVPD che non è integrato con l&#39;applicazione?
   - Quando l&#39;utente avvia l&#39;applicazione, l&#39;utente non viene autenticato tramite il flusso di lavoro Apple SSO. Pertanto, l&#39;applicazione dovrebbe fare riferimento al flusso di autenticazione regolare e presentare il proprio selettore MVPD.
1. Cosa succede se un utente effettua l’accesso andando al *`Settings -> TV Provider`* su iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* sulla sezione tvOS utilizzando un MVPD che ha il *Abilita Single Sign-On* impostare *NO* sulla [Dashboard TVE di Adobe Primetime](https://console.auth.adobe.com/) per la piattaforma iOS/tvOS?
   - Quando l&#39;utente avvia l&#39;applicazione, l&#39;utente non viene autenticato tramite il flusso di lavoro Apple SSO. Pertanto, l&#39;applicazione dovrebbe fare riferimento al flusso di autenticazione regolare e presentare il proprio selettore MVPD.
1. Cosa succede se un utente ha un MVPD non integrato (non supportato) in Apple, ma presente nel selettore Apple?
   - Quando l&#39;utente avvia l&#39;applicazione, l&#39;utente selezionerà solo l&#39;MVPD tramite il flusso di lavoro Apple SSO senza completare il flusso di autenticazione. Pertanto, l&#39;applicazione dovrebbe fare riferimento al flusso di autenticazione regolare, ma potrebbe utilizzare l&#39;MVPD già selezionato.
1. Cosa succede se un utente ha un MVPD che non è integrato (non supportato) in Apple?
   - Quando l&#39;utente avvia l&#39;applicazione, l&#39;utente selezionerà l&#39;opzione di selezione &quot;Altri fornitori TV&quot; tramite il flusso di lavoro Apple SSO. Pertanto, l&#39;applicazione dovrebbe fare riferimento al flusso di autenticazione regolare e presentare il proprio selettore MVPD.
1. Cosa succede se un utente ha un MVPD che viene degradato attraverso il mezzo di [Dashboard TVE di Adobe Primetime](https://console.auth.adobe.com/)?
   - Quando l&#39;utente avvia l&#39;applicazione, l&#39;utente viene autenticato tramite il meccanismo di degradazione e non tramite il flusso di lavoro Apple SSO.
   - L&#39;esperienza dovrebbe essere senza soluzione di continuità per l&#39;utente, mentre l&#39;applicazione verrà informata tramite il *N010* codice di avviso nel caso in cui utilizzi AccessEnabler iOS/tvOS SDK.
1. L&#39;ID utente MVPD cambierà tra Apple SSO e non-Apple SSO flusso di autenticazione?
   - Ci si aspetta che l&#39;ID utente non cambi, ma che debba essere verificato per ogni provider selezionato. 
1. Verrà apportata una modifica ai TTL di autenticazione?
   - L&#39;autenticazione Adobe Primetime continuerà a rispettare i TTL richiesti dai programmatori per la loro integrazione con ogni MVPD.
   - Quando si passa da un&#39;applicazione Programmer a un&#39;altra applicazione Programmer tramite Apple SSO, la seconda applicazione avrà il TTL della sua integrazione Programmer x MVPD corrispondente (non condividerà il TTL della prima applicazione che esegue l&#39;autenticazione)

|  | TTL autenticazione Adobe Primetime scaduto | TTL di autenticazione Adobe Primetime valido |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Token dispositivo Apple TTL scaduto** | L&#39;utente NON è autenticato (dovrebbe apparire il selettore MVPD) | l&#39;utente è autenticato e il TTL è il tempo rimanente del token di autenticazione di Adobe Primetime |
| **TTL token dispositivo Apple valido** | l’utente viene autenticato in modo silenzioso e ottiene un altro token di autenticazione Adobe Primetime con il TTL specificato nel dashboard TVE | l&#39;utente è autenticato e il TTL è il tempo rimanente del token di autenticazione di Adobe Primetime |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
