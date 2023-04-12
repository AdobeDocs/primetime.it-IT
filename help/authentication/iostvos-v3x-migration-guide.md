---
title: Guida alla migrazione a iOS/tvOS v3.x
description: Guida alla migrazione a iOS/tvOS v3.x
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Guida alla migrazione a iOS/tvOS v3.x {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

>[!TIP]
> 
> **Note:**
>
> - A partire dalla versione 3.1 dell’sdk di iOS, le implementazioni possono ora utilizzare WKWebView o UIWebView in modo intercambiabile. Poiché UIWebView è obsoleto, le app devono migrare a WKWebView per evitare problemi con le versioni future di iOS.
> - Nota che la migrazione implicherebbe semplicemente il passaggio della classe UIWebView con WKWebView, non c&#39;è lavoro specifico da fare per quanto riguarda AccessEnabler di Adobe.


</br>

## Aggiorna le impostazioni della build {#update}

Questa versione contiene funzionalità scritte in linguaggio SWIFT. Se l’app è interamente Objective-C, devi impostare la casella di controllo &quot;Incorpora sempre librerie Swift standard&quot; nelle impostazioni di compilazione della destinazione su &quot;Sì&quot;. Quando questa opzione è impostata, Xcode analizza i framework bundle nell&#39;app e, se uno di essi contiene codice Swift, copia le librerie pertinenti nel bundle dell&#39;app. Se non aggiorni le impostazioni di compilazione, l&#39;app potrebbe bloccarsi a causa di errori che indicano che non può caricare AccessEnabler.framework o vari tipi di `ibswift*` librerie.

</br>

## Aggiunta dell&#39;istruzione software {#add}

> Per informazioni su come ottenere l&#39;istruzione software, consultare
> pagina:
> [Registrazione dell&#39;applicazione](/help/authentication/iostvos-application-registration.md)

Una volta ottenuta l&#39;istruzione software, si consiglia di ospitare l&#39;applicazione su un server remoto in modo da poterla revocare o modificarla facilmente senza distribuire una nuova versione dell&#39;applicazione in App Store. All&#39;avvio dell&#39;applicazione, ottenere l&#39;istruzione software dalla posizione remota e passarla nel costruttore AccessEnabler:

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> Informazioni API qui: [Riferimento API di iOS / tvOS](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Aggiungi lo schema URL personalizzato {#add-custom}

> Per informazioni su come ottenere uno schema URL personalizzato, consulta questa pagina: [Ottenere uno schema URL del cliente](/help/authentication/iostvos-application-registration.md)

Dopo aver ottenuto lo schema URL personalizzato, devi aggiungerlo al file info.plist dell&#39;applicazione. Lo schema personalizzato ha questo formato: `adbe.u-XFXJeTSDuJiIQs0HVRAg://`. Quando si aggiunge al file, è necessario omettere i due punti e le barre in avanti. L&#39;esempio precedente diventerà `adbe.u-XFXJeTSDuJiIQs0HVRAg`.

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>CUSTOM_URL_SCHEME_HERE</string>
            </array>
        </dict>
    </array>
```

</br>

## Intercettazione delle chiamate allo schema URL personalizzato {#intercept}

Ciò si applica solo nel caso in cui l&#39;applicazione abbia precedentemente abilitato la gestione manuale di Safari View Controller (SVC) tramite [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](/help/authentication/iostvos-sdk-api-reference.md) chiama e per MVPD specifici che richiedono Safari View Controller (SVC), quindi richiedono il caricamento degli URL degli endpoint di autenticazione e logout da parte di un controller SFSafariViewController invece di un controller UIWebView/WKWebView.

Durante i flussi di autenticazione e logout l&#39;applicazione deve monitorare l&#39;attività del `SFSafariViewController `controllore mentre passa attraverso diversi reindirizzamenti. L&#39;applicazione deve rilevare il momento in cui carica un URL personalizzato specifico definito dalla `application's custom URL scheme` (ad esempio`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`. Quando il controller carica questo URL personalizzato specifico, l&#39;applicazione deve chiudere la `SFSafariViewController` e chiama AccessEnabler `handleExternalURL:url `Metodo API.

Nel tuo `AppDelegate` aggiungi il seguente metodo:

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> Informazioni API qui: [Gestisci URL esterno](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Aggiorna la firma del metodo setRequestor {#update-setreq}

Poiché il nuovo SDK utilizza un nuovo meccanismo di autenticazione, non è necessario il parametro signedRequestId o la chiave pubblica e il segreto (per tvOS). La `setRequestor` viene semplificato e richiede solo requestorID.

### iOS

Questo codice:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

diventa:

```swift
    accessEnabler.setRequestor(requestorId)
```

</br>

### tvOS

Questo codice:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId,
                    secret: "secret", publicKey: "public_key")
```

diventa:

```swift
    accessEnabler.setRequestor(requestorId)
```

> Informazioni API qui: [Imposta Richiedente](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Sostituisci il metodo getAuthenticationToken con il metodo handleExternalURL {#replace}

`getAuthentication` è stato utilizzato in passato per completare il flusso di autenticazione. Poiché il suo nome era fuorviante, è stato rinominato in `handleExternalURL` e prende l’url come parametro.

Modifica tutte le occorrenze:

```swift
    accessEnabler.getAuthenticationToken()
```

in questo:

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> Informazioni API qui: [Gestisci URL esterno](/help/authentication/iostvos-sdk-api-reference.md)
