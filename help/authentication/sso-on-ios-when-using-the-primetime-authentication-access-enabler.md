---
title: SSO su iOS quando si utilizza l’attivatore di accesso per l’autenticazione Primetime
description: SSO su iOS quando si utilizza l’attivatore di accesso per l’autenticazione Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# SSO su iOS quando si utilizza l’attivatore di accesso per l’autenticazione Primetime {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Panoramica

Il Single Sign-On (SSO) tra le app basate sull’autenticazione di Primetime funziona in modi diversi a seconda del sistema operativo sottostante.

Questo documento si rivolge **SSO su iOS**, quando si utilizza l’autenticazione Adobe Primetime **Access Enabler**.

**Access Enabler** **1,10** è la versione più recente dell’SDK nativo per iOS per l’autenticazione di Adobe Primetime. L’Adobe consiglia vivamente di passare a questa versione, anziché utilizzare una versione precedente. Se si utilizza una versione precedente di Access Enabler, è possibile scaricare la versione più recente [qui](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

L’SSO su iOS è determinato dalle seguenti condizioni:

- Le app devono utilizzare lo stesso **archiviazione token** (sotto forma di un tavolo di montaggio personalizzato creato da Access Enabler).
- Le app devono generare lo stesso **ID dispositivo** Access Enabler calcola l&#39;ID dispositivo in base all&#39;indirizzo MAC o IDFV, a seconda della versione del sistema operativo.

## Comportamento

Il comportamento SSO è il seguente:

- **iOS 6 e versioni precedenti**: SSO funziona automaticamente tra app sviluppate dallo stesso team o da team diversi. L’ID dispositivo viene calcolato in base all’indirizzo MAC (lo stesso valore viene prodotto in tutte le app) e l’area di archiviazione è comune a tutte le app (il tavolo di montaggio personalizzato è condivisibile tra le app in iOS 6 e versioni successive).
   - **Importante:** Tieni presente che la versione 1.9.4 dell’SDK iOS ha [è stato aumentato il target minimo di implementazione di iOS ad iOS 7.](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library)
- **iOS 7 e versioni successive**: l’SSO funziona nelle seguenti condizioni:

1. Le app vengono pubblicate utilizzando lo stesso profilo di distribuzione Apple o profili che appartengono allo stesso team. Questo è l&#39;unico modo in cui le app possono condividere bacheche personalizzate su iOS 7 e versioni successive. In tutti gli altri scenari, il tavolo di montaggio è in modalità sandbox per applicazione. Da [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html): \+\[UIPasteboardPasteboardWithName:create:\] e +\[UIPasteboard pasteboardWithUniqueName\] ora assegnano un nome univoco a tutte le app dello stesso gruppo di applicazioni che possono accedere al tavolo di montaggio. Se lo sviluppatore tenta di creare un tavolo di montaggio con un nome che esiste già e non fa parte della stessa suite di app, otterrà il proprio tavolo di montaggio univoco e privato. Tieni presente che questo non influisce sul sistema di pastboard fornito, generale e trova.

1. Le app hanno lo stesso prefisso dell’ID bundle (tutti i componenti tranne l’ultimo). Solo le applicazioni che condividono lo stesso prefisso Bundle ID calcoleranno lo stesso valore IDFV. Da [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#//apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor): in IOS 7, tutti i componenti del bundle a eccezione dell’ultimo componente vengono utilizzati per generare l’ID fornitore. Se l’ID bundle ha un solo componente, viene utilizzato l’intero ID bundle.

Ora concentriamoci sulla **&quot;iOS 7 e versioni successive&quot;** poiché è la più frequente per gli utenti reali:

Entrambe le condizioni (condivisione di un profilo dallo stesso team di sviluppo e presenza di un prefisso di identificatore bundle comune) sono condizioni obbligatorie per l’SSO.

Di seguito sono elencate le possibili combinazioni e i risultati ottenuti:

- **Profili dello stesso team e prefisso dello stesso ID bundle**: le app condivideranno lo stesso archivio su tavolo e avranno lo stesso ID dispositivo (IDFV). Un utente dovrà effettuare l’autenticazione una sola volta (nella prima app utilizzata) e lo stato di autenticazione verrà condiviso tra tutte le altre app. Flusso di esempio:

1. L’utente apre l’app A (con ID bundle) *com.x.y.AppA*) e non è autenticato
1. L’utente esegue l’autenticazione nell’app A
1. L’utente apre l’app B (con ID bundle) *com.x.y.AppB*) e viene autenticato automaticamente condividendo i dati di adesione dall&#39;app A (dal passaggio 2)
1. L’utente apre l’app A ed è ancora autenticato (dal passaggio 2)



- **Profili dello stesso team ma con prefissi di ID bundle diversi**: le app condivideranno lo stesso archivio su tavolo ma avranno ID dispositivo (IDFV) diversi. Un utente dovrà effettuare l’autenticazione una volta per ogni app. Flusso di esempio:

1. L’utente apre l’app A (con ID bundle) *com.x.y.AppA*) e non è autenticato
1. L’utente esegue l’autenticazione nell’app A
1. L’utente apre l’app B (con ID bundle) *com.z.AppB*) e Access Enabler rileva il token ottenuto dalla prima app (perché lo storage è condiviso), ma non tenta di utilizzarlo tramite SSO a causa dei diversi ID dispositivo
1. L’utente esegue l’autenticazione nell’app B
1. L’utente apre l’app A ed è ancora autenticato (dal passaggio 2)



- **Profili di team diversi (l’ID bundle è irrilevante in questo scenario)**: le app avranno archivi diversi sulla bacheca e l’SSO verrà disabilitato tra di essi. Un utente dovrà effettuare l’autenticazione una volta per ogni app e le sessioni di autenticazione rimarranno permanenti quando si passa da un’app all’altra. Flusso di esempio:


1. L’utente apre l’app A e non è autenticato
1. L’utente esegue l’autenticazione nell’app A
1. L’utente apre l’app B e non è autenticato
1. L’utente esegue l’autenticazione nell’app B
1. L’utente apre l’app A ed è autenticato (dal passaggio 2)
1. L’utente apre l’app B ed è autenticato (dal passaggio 4)

**Nota:** Si noti che le condizioni sopra riportate per l&#39;SSO sono applicabili quando si installano applicazioni tramite **Apple App Store**. Se le app sono distribuite su un simulatore (in cui non è applicabile la firma dell’app), installate con Xcode o distribuite tramite un profilo Ad Hoc, puoi ottenere risultati diversi.

**Importante:** Nota (**Informazioni su AccessEnabler v1.8**): il secondo scenario descritto in precedenza (profili dello stesso team ma con prefissi di ID bundle diversi) creerà un’esperienza utente molto sgradevole per gli utenti di **AccessEnabler v1.8** tra applicazioni sviluppate dallo stesso team (media company). L’utente verrà disconnesso automaticamente durante la transizione tra le app della stessa media company, pertanto gli sviluppatori di applicazioni devono prestare attenzione quando decidono l’ID bundle e il profilo di distribuzione. Lo scenario esatto in questo caso è presentato di seguito:

Le app condivideranno lo stesso archivio in bacheca, ma avranno ID dispositivo diversi (IDFV, Device ID). Un utente dovrà effettuare l’autenticazione una volta per ogni app, **ma le sessioni di autenticazione verranno cancellate quando si passa da un’app all’altra**. Flusso di esempio:

1. L’utente apre l’app A (con ID bundle) *com.x.y.AppA*) e non è autenticato
1. L’utente esegue l’autenticazione nell’app A
1. L’utente apre l’app B (con ID bundle) *com.z.AppB*) e i dati di adesione creati dall&#39;app A vengono automaticamente cancellati dall&#39;Access Enabler (meccanismo di sicurezza che rileva un conflitto tra l&#39;ID dispositivo attualmente calcolato nell&#39;app B e quello memorizzato nei token di adesione, creato dall&#39;app A)
1. L’utente esegue l’autenticazione nell’app B
1. L’utente apre l’app A e i dati di adesione creati dall’app B vengono automaticamente cancellati dall’Access Enabler (meccanismo di sicurezza che rileva un conflitto tra l’ID dispositivo attualmente calcolato nell’app A e quello memorizzato nei token di adesione, creato dall’app B)
