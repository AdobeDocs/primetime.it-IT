---
title: Cookie Apple SSO (REST API)
description: Cookie Apple SSO (REST API)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# Cookie Apple SSO (REST API) {#apple-sso-cookbook-rest-api}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#Introduction}

L&#39;API REST di autenticazione di Adobe Primetime può supportare l&#39;autenticazione Single Sign-On (SSO) della piattaforma per gli utenti finali di applicazioni client in esecuzione su iOS, iPadOS o tvOS attraverso quello che chiamiamo flusso di lavoro SSO di Apple.

Nota che questo documento funge da estensione alla documentazione REST API esistente, che può essere trovata [qui](/help/authentication/rest-api-reference.md).

</br>

## Cookie {#Cookbooks}

Per poter beneficiare dell’esperienza utente Apple SSO, un’applicazione deve integrare la [Account utente con sottoscrizione video](https://developer.apple.com/documentation/videosubscriberaccount) framework sviluppato da Apple, mentre per quanto riguarda la comunicazione API REST di autenticazione di Adobe Primetime, dovrebbe seguire la sequenza di suggerimenti riportati di seguito.

</br>

### Autenticazione {#Authentication}

- [Esiste un token di autenticazione Adobe valido?](#Is_there_a_valid_Adobe_authentication_token)
- [L’utente ha effettuato l’accesso tramite Platform SSO?](#Is_the_user_logged_in_via_Platform_SSO)
- [Recupera configurazione Adobe](#Fetch_Adobe_configuration)
- [Avviare il flusso di lavoro SSO di Platform con la configurazione di Adobe](#Initiate_Platform_SSO_workflow_with_Adobe_config)
- [L&#39;accesso dell&#39;utente ha esito positivo?](#Is_user_login_successful)
- [Ottieni una richiesta di profilo dall&#39;Adobe per l&#39;MVPD selezionato](#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD)
- [Inoltra la richiesta di Adobe a Platform SSO per ottenere il profilo](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile)
- [Scambiare il profilo SSO di Platform per un token di autenticazione Adobe](#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token)
- [Il token di Adobe è generato correttamente?](#Is_Adobe_token_generated_successfully)
- [Avvia flusso di lavoro di autenticazione a seconda schermata](#Initiate_second_screen_authentication_workflow)
- [Procedi con flussi di autorizzazione](#Proceed_with_authorization_flows)

 

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/qu/platform-sso.jpeg)

</br>

#### Passaggio: &quot;Esiste un token di autenticazione Adobe valido?&quot; {#Is_there_a_valid_Adobe_authentication_token}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite [Autenticazione Adobe Primetime](/help/authentication/check-authentication-token.md) servizio.

</br>

#### Passaggio: &quot;L’utente ha effettuato l’accesso tramite Platform SSO?&quot; {#Is_the_user_logged_in_via_Platform_SSO}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite [Account utente con sottoscrizione video](https://developer.apple.com/documentation/videosubscriberaccount) struttura.

- La domanda dovrebbe verificare [autorizzazione di accesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) le informazioni di abbonamento dell&#39;utente e procedere solo se l&#39;utente lo ha autorizzato.
- La domanda deve presentare un [richiesta](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) per informazioni sull&#39;account utente iscritto.
- L&#39;applicazione dovrebbe attendere ed elaborare il [metadati](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) informazioni.

 

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Seguire lo snippet di codice e prestare maggiore attenzione ai commenti.

```swift
...
let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();

videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
            switch (accessStatus) {
            // The user allows the application to access subscription information.
            case VSAccountAccessStatus.granted:
                    // Construct the request for subscriber account information.
                    let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();

                    // This is actually the SAML Issuer not the channel ID.
                    vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAccountProviderIdentifier = true;
                    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                    
                    // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                    vsaMetadataRequest.isInterruptionAllowed = false;
                    
                    // Submit the request for subscriber account information - accountProviderIdentifier.
                    videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in        
                        if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                            // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                            // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                            ...
                            // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                            // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                            ...
                            // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                            // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                            ...
                            // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                            ...
                            // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                            ...
                        } else {
                            // The user is not authenticated at platform level, continue with the "Fetch Adobe configuration" step.
                            ...
                        }
                    }
        
            // The user has not yet made a choice or does not allow the application to access subscription information.
            default:
                // Fallback to regular authentication workflow.
                ...
            }
}
...  
```

</br>

#### Passaggio: &quot;Recupera configurazione Adobe&quot; {#Fetch_Adobe_configuration}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite [Autenticazione Adobe Primetime](/help/authentication/provide-mvpd-list.md) servizio.


>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Tieni presente le proprietà MVPD: *`enablePlatformServices`*, *`boardingStatus`*, *`displayInPlatformPicker`*, *`platformMappingId`*, *`requiredMetadataFields`* e prestare maggiore attenzione ai commenti presentati in frammenti di codice da altre fasi.

</br>

#### Passaggio &quot;Avvia il flusso di lavoro SSO di Platform con Adobe config&quot; {#Initiate_Platform_SSO_workflow_with_Adobe_config}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite [Account utente con sottoscrizione video](https://developer.apple.com/documentation/videosubscriberaccount) struttura.

- La domanda dovrebbe verificare [autorizzazione di accesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) le informazioni di abbonamento dell&#39;utente e procedere solo se l&#39;utente lo ha autorizzato.
- La domanda deve fornire un [delegato](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) per VSAccountManager.
- La domanda deve presentare un [richiesta](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) per informazioni sull&#39;account utente iscritto.
- L&#39;applicazione dovrebbe attendere ed elaborare il [metadati](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) informazioni.

 

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Seguire lo snippet di codice e prestare maggiore attenzione ai commenti.


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    // This must be a class implementing the VSAccountManagerDelegate protocol.
    let videoSubscriberAccountManagerDelegate: VideoSubscriberAccountManagerDelegate = VideoSubscriberAccountManagerDelegate();
    
    videoSubscriberAccountManager.delegate = videoSubscriberAccountManagerDelegate;
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to prompt the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = true;
                        
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to filter the TV providers from the Apple picker.
                        vsaMetadataRequest.supportedAccountProviderIdentifiers = supportedAccountProviderIdentifiers;
    
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to sort the TV providers from the Apple picker.
                        if #available(iOS 11.0, tvOS 11, *) {
                            vsaMetadataRequest.featuredAccountProviderIdentifiers = featuredAccountProviderIdentifiers;
                        }
                        
                        // Submit the request for subscriber account information - accountProviderIdentifier.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in                        
                            // This represents the checks for the "Is user login successful?" step.
                            if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                                // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                                // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                                ...
                                // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                                // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                                ...
                                // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                                // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                                ...
                                // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                                ...
                                // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                                ...
                            } else {
                                // The user is not authenticated at platform level.
                                if (vsaError != nil) {
                                    // The application can check to see if the user selected a provider which is present in Apple picker, but the provider is not onboarded in platform SSO.
                                    if let error: NSError = (vsaError! as NSError), error.code == 1, let appleMsoId = error.userInfo["VSErrorInfoKeyUnsupportedProviderIdentifier"] as! String? {
                                        var mvpd: Mvpd? = nil;
    
                                        // The requestor.mvpds must be computed during the "Fetch Adobe configuration" step. 
                                        for provider in requestor.mvpds {
                                            if provider.platformMappingId == appleMsoId {
                                                mvpd = provider;
                                                break;
                                            }
                                        }
                                        
                                        if mvpd != nil {
                                            // Continue with the "Initiate second screen authentcation workflow" step, but you can skip prompting the user with your MVPD picker and use the mvpd selection, therefore creating a better UX.
                                            ...
                                        } else {
                                            // Continue with the "Initiate second screen authentcation workflow" step.
                                            ...
                                        }
                                    } else {
                                        // Continue with the "Initiate second screen authentcation workflow" step.
                                        ...
                                    }
                                } else {
                                    // Continue with the "Initiate second screen authentcation workflow" step.
                                    ...
                                }
                            }
                        }
            
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### Passaggio: &quot;L&#39;accesso dell&#39;utente ha esito positivo?&quot; {#Is_user_login_successful}

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Tieni presente lo snippet di codice dal [&quot;Avvia il flusso di lavoro SSO di Platform con Adobe config&quot;](#Initiate_Platform_SSO_workflow_with_Adobe_config) passo. L&#39;accesso dell&#39;utente ha esito positivo nel caso in cui il *`vsaMetadata!.accountProviderIdentifier`* contiene un valore valido e la data corrente non ha superato il *`vsaMetadata!.authenticationExpirationDate`* valore.

</br>

#### Passaggio &quot;Ottieni una richiesta di profilo dall&#39;Adobe per l&#39;MVPD selezionato&quot; {#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite l’autenticazione Adobe Primetime [Richiesta profilo](/help/authentication/retrieve-profilerequest.md) servizio.

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** L&#39;identificatore del provider ottenuto dal framework dell&#39;account utente con sottoscrizione video rappresenta il *`platformMappingId`* in termini di configurazione dell’autenticazione Adobe Primetime. Pertanto, l&#39;applicazione deve determinare il valore della proprietà MVPD id, utilizzando *`platformMappingId`* tramite autenticazione Adobe Primetime [Fornire l&#39;elenco MVPD](/help/authentication/provide-mvpd-list.md) servizio.

</br>

#### Passaggio: &quot;Inoltra la richiesta di Adobe a Platform SSO per ottenere il profilo&quot; {#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite [Account utente con sottoscrizione video](https://developer.apple.com/documentation/videosubscriberaccount) struttura.


- La domanda dovrebbe verificare [autorizzazione di accesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) le informazioni di abbonamento dell&#39;utente e procedere solo se l&#39;utente lo ha autorizzato.
- La domanda deve presentare un [richiesta](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) per informazioni sull&#39;account utente iscritto.
- L&#39;applicazione dovrebbe attendere ed elaborare il [metadati](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) informazioni.

 

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Seguire lo snippet di codice e prestare maggiore attenzione ai commenti.

```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = false;
    
                        // This are the user metadata fields expected to be available on a successful login and are determined from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service. Look for the requiredMetadataFields associated with the provider determined in a previous step.
                        vsaMetadataRequest.attributeNames = requiredMetadataFields;
    
                        // This is the payload from [Adobe Primetime Authentication](/help/authentication/retrieve-profilerequest.md) service.
                        vsaMetadataRequest.verificationToken = profileRequestPayload;
                        
                        // Submit the request for subscriber account information.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in
                            if (vsaMetadata != nil && vsaMetadata!.samlAttributeQueryResponse != nil) {
                                var samlResponse: String? = vsaMetadata!.samlAttributeQueryResponse!;
                                
                                // Remove new lines, new tabs and spaces.
                                samlResponse = samlResponse?.replacingOccurrences(of: "[ \\t]+", with: " ", options: String.CompareOptions.regularExpression);
                                samlResponse = samlResponse?.components(separatedBy: CharacterSet.newlines).joined(separator: "");
                                samlResponse = samlResponse?.trimmingCharacters(in: CharacterSet.whitespacesAndNewlines);
                                
                                // Base64 encode.
                                samlResponse = samlResponse?.data(using: .utf8)?.base64EncodedString(options: []);
                                
                                // URL encode. Please be aware not to double URL encode it further.
                                samlResponse = samlResponse?.addingPercentEncoding(withAllowedCharacters: CharacterSet.init(charactersIn: "!*'();:@&=+$,/?%#[]").inverted);
                                
                                // Continue with the "Exchange the Platform SSO profile for an Adobe authentication token" step.
                                ...
                            } else {
                                // Fallback to regular authentication workflow.
                                ...
                            }
                        }
                        
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### Passaggio: &quot;Scambiare il profilo SSO di Platform per un token di autenticazione di Adobe&quot; {#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite l’autenticazione Adobe Primetime [Token Exchange](/help/authentication/token-exchange.md) servizio.


>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Tieni presente lo snippet di codice dal [&quot;Inoltra la richiesta di Adobe a Platform SSO per ottenere il profilo&quot;](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile) passo. Questo *`vsaMetadata!.samlAttributeQueryResponse!`* rappresenta *`SAMLResponse`*, che deve essere trasmesso [Token Exchange](/help/authentication/token-exchange.md) e richiede la manipolazione e la codifica delle stringhe (*Base64* codificati e *URL* codificato successivamente) prima di effettuare la chiamata .

</br>

#### Passaggio: &quot;Il token di Adobe è generato correttamente?&quot; {#Is_Adobe_token_generated_successfully}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite l’autenticazione Adobe Primetime media [Token Exchange](/help/authentication/token-exchange.md) una risposta di successo, che sarà *`204 No Content`*, che indica che il token è stato creato correttamente ed è pronto per essere utilizzato per i flussi di autorizzazione.

</br>

#### Passaggio: &quot;Avvia flusso di lavoro di autenticazione a seconda schermata&quot; {#Initiate_second_screen_authentication_workflow}

**Importante:** La terminologia del &quot;flusso di lavoro di autenticazione secondo schermo&quot; è appropriata per AppleTV, mentre la terminologia del &quot;flusso di lavoro di autenticazione primo schermo&quot; / &quot;flusso di lavoro di autenticazione regolare&quot; sarebbe più appropriata per iPhone e iPad.


>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite l’autenticazione Adobe Primetime

[Richiesta codice di registrazione](/help/authentication/registration-code-request.md), [Avvia autenticazione](/help/authentication/initiate-authentication.md) e [Token di autenticazione per recupero API REST](/help/authentication/retrieve-authentication-token.md) o [Verifica token di autenticazione](/help/authentication/check-authentication-token.md) servizi.


>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Segui i passaggi riportati di seguito per l&#39;implementazione o le implementazioni tvOS.

- La domanda deve [ottenere un codice di registrazione](/help/authentication/registration-code-request.md) e presentarlo all&#39;utente finale sul primo dispositivo (schermo).
- L&#39;applicazione dovrebbe essere avviata [polling per riconoscere lo stato di autenticazione](/help/authentication/retrieve-authentication-token.md) sul primo dispositivo (schermo) dopo aver ottenuto il codice di registrazione.
- Un&#39;altra applicazione dovrebbe [avvia autenticazione](/help/authentication/initiate-authentication.md) su un secondo dispositivo (schermo) quando viene utilizzato il codice di registrazione.
- L&#39;applicazione deve cessare [sondaggio](/help/authentication/retrieve-authentication-token.md) sul primo dispositivo (schermo) quando viene generato il token di autenticazione.

 

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Segui i passaggi riportati di seguito per l’implementazione di iOS/iPadOS.

- La domanda deve [ottenere un codice di registrazione](/help/authentication/registration-code-request.md) che non deve essere presentata all’utente finale sul primo dispositivo (schermo).
- La domanda deve [avvia autenticazione](/help/authentication/initiate-authentication.md) sul primo dispositivo (schermo) utilizzando il codice di registrazione e un [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) o [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) componente.
- L&#39;applicazione dovrebbe essere avviata [sondaggio per conoscere lo stato di autenticazione](/help/authentication/retrieve-authentication-token.md) sul primo dispositivo (schermo) dopo il [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) o [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) viene chiuso.
- L&#39;applicazione deve cessare [sondaggio](/help/authentication/retrieve-authentication-token.md) sul primo dispositivo (schermo) quando viene generato il token di autenticazione.

</br>

#### Passaggio: &quot;Procedi con flussi di autorizzazione&quot; {#Proceed_with_authorization_flows}

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite l’autenticazione Adobe Primetime [Avvia autorizzazione](/help/authentication/initiate-authorization.md) e [Ottieni token multimediale breve](/help/authentication/obtain-short-media-token.md) servizi.

</br>

### Logout {#Logout}

La [Account utente con sottoscrizione video](https://developer.apple.com/documentation/videosubscriberaccount) framework non fornisce un&#39;API per disconnettersi programmaticamente le persone che hanno effettuato l&#39;accesso al proprio account del provider TV a livello di sistema del dispositivo. Pertanto, affinché l’logout abbia effetto completo, l’utente finale dovrà esplicitamente disconnettersi da *`Settings -> TV Provider`* su iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* su tvOS. L&#39;altra opzione che l&#39;utente dovrebbe avere è quella di revocare il permesso di accedere alle informazioni di abbonamento dell&#39;utente dalla sezione specifica impostazioni dell&#39;applicazione (Accesso provider TV).

>[!TIP]
>
> **<u>Suggerimento:</u>** Implementalo tramite l’autenticazione Adobe Primetime [Chiamata a metadati utente](/help/authentication/user-metadata.md) e [Logout](/help/authentication/initiate-logout.md) servizi.


>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Segui i passaggi riportati di seguito per l&#39;implementazione o le implementazioni tvOS.
 

- L&#39;applicazione deve determinare se l&#39;autenticazione è avvenuta in seguito a un accesso tramite la piattaforma SSO o meno, utilizzando il &quot;*tokenSource&quot;* [metadati utente](/help/authentication/user-metadata.md) dal servizio di autenticazione di Adobe Primetime.
- L&#39;applicazione deve istruire/richiedere all&#39;utente di disconnettersi in modo esplicito da *`Settings -> Accounts -> TV Provider`* su tvOS **only** nel caso in cui *&quot;tokenSource&quot;* è uguale a &quot;*Apple&quot;.*
- La domanda deve [avvia il logout](/help/authentication/initiate-logout.md) dal servizio di autenticazione di Adobe Primetime utilizzando una chiamata HTTP diretta. Questo non faciliterebbe la pulizia delle sessioni sul lato MVPD.

 

>[!TIP]
>
> **<u>Suggerimento Pro:</u>** Segui i passaggi riportati di seguito per l’implementazione di iOS/iPadOS.

- L&#39;applicazione deve determinare se l&#39;autenticazione è avvenuta in seguito a un accesso tramite la piattaforma SSO o no, utilizzando il &quot;*tokenSource&quot;* [metadati utente](/help/authentication/user-metadata.md) dal servizio di autenticazione di Adobe Primetime.
- L&#39;applicazione deve istruire/richiedere all&#39;utente di disconnettersi in modo esplicito da *`Settings -> TV Provider`* su iOS/iPadOS **only** nel caso in cui *&quot;tokenSource&quot;* è uguale a *&quot;Apple&quot;*.
- La domanda deve [avvia il logout](/help/authentication/initiate-logout.md) dal servizio di autenticazione di Adobe Primetime utilizzando un [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) o [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) componente. Questo faciliterebbe la pulizia delle sessioni sul lato MVPD.

<!--

## Resources

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [REST API Overview](/help/authentication/rest-api-overview.md)
- [REST API Cookbook (Server-to-Server)](/help/authentication/rest-api-cookbook-servertoserver.md)
- [REST API Cookbook (Client-to-Server)](/help/authentication/rest-api-cookbook-clienttoserver.md)
- [REST API Reference](/help/authentication/rest-api-reference.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->

