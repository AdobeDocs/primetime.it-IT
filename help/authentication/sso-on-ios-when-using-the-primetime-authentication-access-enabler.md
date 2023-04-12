---
title: SSO su iOS quando si utilizza Primetime Authentication Access Enabler
description: SSO su iOS quando si utilizza Primetime Authentication Access Enabler
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---


# SSO su iOS quando si utilizza Primetime Authentication Access Enabler {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Panoramica

Il Single Sign-On (SSO) tra le app con tecnologia di autenticazione Primetime funziona in modi diversi a seconda del sistema operativo sottostante.

Questo documento contiene **SSO su iOS**, quando si utilizza l’autenticazione Adobe Primetime **Access Enabler**.

**Access Enabler** **1,10** è la versione più recente dell’SDK nativo di iOS per l’autenticazione di Adobe Primetime. L’Adobe consiglia vivamente di passare a questa versione anziché rimanere con una versione precedente. Se utilizzi una versione precedente di Access Enabler, puoi scaricare la versione più recente [qui](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

SSO su iOS è dettato dalle seguenti condizioni:

- Le app devono utilizzare gli stessi **memoria token** (sotto forma di cartone personalizzato creato da Access Enabler).
- Le app devono generare gli stessi **ID dispositivo** (Access Enabler calcola l&#39;ID dispositivo in base all&#39;indirizzo MAC o all&#39;ID, a seconda della versione del sistema operativo).

## Comportamento

Il comportamento dell&#39;SSO è il seguente:

- **iOS 6 e versioni precedenti**: SSO funziona automaticamente tra app sviluppate dallo stesso team o da team diversi. L&#39;ID dispositivo viene calcolato in base all&#39;indirizzo MAC (lo stesso valore viene prodotto in tutte le app) e l&#39;area di archiviazione è comune a tutte le app (il tavolo di montaggio personalizzato è condivisibile nelle app in iOS 6 e versioni precedenti).
   - **Importante:** Nota che la versione iOS SDK 1.9.4 è [è stato aumentato il target minimo di distribuzione iOS ad iOS 7.](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS 7 e versioni successive**: L&#39;SSO funzionerà nelle seguenti condizioni:

1. Le app vengono pubblicate utilizzando lo stesso profilo di distribuzione di Apple o profili che appartengono allo stesso team. Questo è l&#39;unico modo per le app di condividere pannelli di gestione personalizzati su iOS 7 e superiori. In tutti gli altri scenari, il tavolo di pasto è sandbox per applicazione. Da [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html): \+\[Psteboard di UIPasteboardWithName:create:\] e +\[UIPasteboard pasteboardWithUniqueName\] ora uniscono il nome dato per consentire solo alle app dello stesso gruppo di applicazioni di accedere al tavolo di montaggio. Se lo sviluppatore tenta di creare un tavolo di montaggio con un nome già esistente e non fanno parte della stessa suite di app, ottiene il proprio pannello di controllo unico e privato. Tieni presente che questo non influisce sul sistema fornito di pannelli, pannelli generali e trova.

1. Le app hanno lo stesso prefisso Bundle ID (tutti i componenti eccetto l’ultimo). Solo le applicazioni che condividono lo stesso prefisso Bundle ID calcoleranno lo stesso IDFV. Da [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#//apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor): In IOS 7, tutti i componenti del bundle eccetto l&#39;ultimo componente vengono utilizzati per generare l&#39;ID fornitore. Se l&#39;ID del bundle ha un solo componente, viene utilizzato l&#39;intero ID del bundle.

Ora concentriamoci sul **&quot;iOS 7 e versioni successive&quot;** scenario, poiché è il più frequente per gli utenti reali:

Entrambe le condizioni (la condivisione di un profilo dallo stesso team di sviluppo e con un prefisso comune per l’identificatore del bundle) sono condizioni obbligatorie per l’SSO.

Di seguito sono elencate le possibili combinazioni e i relativi risultati ottenuti:

- **Profili dello stesso team e lo stesso prefisso Bundle ID**: le app condivideranno lo stesso archivio di cartone e avranno lo stesso ID dispositivo (IDFV). Un utente dovrà eseguire l&#39;autenticazione una sola volta (nella prima app utilizzata) e lo stato di autenticazione sarà condiviso tra tutte le altre app. Esempio di flusso:

1. L&#39;utente apre l&#39;app A (con Bundle ID) *com.x.y.AppA*) e non è autenticato
1. L&#39;utente esegue l&#39;autenticazione nell&#39;app A
1. L&#39;utente apre l&#39;app B (con Bundle ID) *com.x.y.AppB*) e viene autenticata automaticamente condividendo i dati di adesione dall&#39;app A (dal passaggio 2)
1. L&#39;utente apre l&#39;app A ed è ancora autenticato (dal passaggio 2)

 

- **Profili dello stesso team ma diversi prefissi Bundle ID**: le app condivideranno lo stesso archivio di pannelli, ma avranno diversi ID dispositivo (IDFV). Un utente dovrà eseguire l&#39;autenticazione una volta per ogni app. Esempio di flusso:

1. L&#39;utente apre l&#39;app A (con Bundle ID) *com.x.y.AppA*) e non è autenticato
1. L&#39;utente esegue l&#39;autenticazione nell&#39;app A
1. L&#39;utente apre l&#39;app B (con Bundle ID) *com.z.AppB*) e Access Enabler rileva il token ottenuto dalla prima app (perché l&#39;archiviazione è condivisa) ma non tenterà di utilizzarlo tramite SSO a causa dei diversi ID dispositivo
1. L&#39;utente esegue l&#39;autenticazione nell&#39;app B
1. L&#39;utente apre l&#39;app A ed è ancora autenticato (dal passaggio 2)

 

- **Profili da team diversi (il Bundle ID è irrilevante in questo scenario)**: le app avranno diversi archivi di cartone e l&#39;SSO sarà disabilitato tra loro. Un utente dovrà eseguire l&#39;autenticazione una volta per ogni app e le sessioni di autenticazione rimarranno costanti quando si passa da un&#39;app all&#39;altra. Esempio di flusso:


1. L&#39;utente apre l&#39;app A e non è autenticato
1. L&#39;utente esegue l&#39;autenticazione nell&#39;app A
1. L&#39;utente apre l&#39;app B e non è autenticato
1. L&#39;utente esegue l&#39;autenticazione nell&#39;app B
1. L&#39;utente apre l&#39;app A e viene autenticato (dal passaggio 2)
1. L&#39;utente apre l&#39;app B ed è autenticato (dal passaggio 4)

**Nota:** Si prega di notare che le condizioni di cui sopra per l&#39;SSO sono applicabili quando si installano applicazioni attraverso **Apple App Store**. Se le app sono distribuite su un simulatore (dove la firma dell&#39;app non è applicabile), installate con Xcode o distribuite tramite un profilo Ad Hoc, è possibile ottenere risultati diversi.

**Importante:** Nota (**riguardante AccessEnabler v1.8**): Il secondo scenario descritto sopra (profili dello stesso team ma diversi prefissi Bundle ID) creerà un’esperienza utente molto spiacevole per gli utenti del **AccessEnabler v1.8** tra le applicazioni sviluppate dallo stesso team (media company). L’utente verrà disconnesso automaticamente durante la transizione tra app dalla stessa società di media, pertanto gli sviluppatori di applicazioni devono prestare attenzione quando decidono il Bundle ID e il profilo di distribuzione. Lo scenario esatto in questo caso è presentato di seguito:

Le app condivideranno lo stesso archivio di pannelli, ma avranno diversi ID dispositivo (IDFV). Un utente dovrà eseguire l&#39;autenticazione una volta per ogni app, **ma le sessioni di autenticazione verranno cancellate quando si passa da un&#39;app all&#39;altra**. Esempio di flusso:

1. L&#39;utente apre l&#39;app A (con Bundle ID) *com.x.y.AppA*) e non è autenticato
1. L&#39;utente esegue l&#39;autenticazione nell&#39;app A
1. L&#39;utente apre l&#39;app B (con Bundle ID) *com.z.AppB*) e i dati di adesione creati dall&#39;app A vengono cancellati automaticamente da Access Enabler (meccanismo di sicurezza che rileva uno scontro tra l&#39;ID dispositivo attualmente calcolato nell&#39;app B e quello memorizzato nei token di adesione - creato dall&#39;app A)
1. L&#39;utente esegue l&#39;autenticazione nell&#39;app B
1. L&#39;utente apre l&#39;app A e i dati di adesione creati dall&#39;app B vengono automaticamente cancellati dall&#39;Access Enabler (meccanismo di sicurezza che rileva uno scontro tra l&#39;ID dispositivo attualmente calcolato nell&#39;app A e quello memorizzato nei token di adesione, creato dall&#39;app B)

