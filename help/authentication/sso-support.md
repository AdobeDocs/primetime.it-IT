---
title: Supporto Single Sign-On
description: Supporto Single Sign-On
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Supporto Single Sign-On

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview-sso-support}

Questo documento descrive i tipi di Single Sign On supportati e gestiti dall&#39;autenticazione Adobe Primetime su piattaforme diverse. Lo scopo di questo documento è quello di chiarire ciò che è supportato e ciò che non lo è, qual è la copertura MVPD per ogni metodo SSO e ciò che è richiesto dai programmatori per poter beneficiare dell&#39;SSO su ogni piattaforma.

Dopo che un utente accede con le proprie credenziali MVPD, Adobe Primetime Authentication genera un token sicuro che rappresenta la sessione di autenticazione dell&#39;MVPD e lo lega al dispositivo dell&#39;utente utilizzando un ID dispositivo. L’autenticazione Adobe Primetime memorizza il token o l’ID dispositivo su un server o sul dispositivo. Ciò consente agli utenti di immettere le proprie credenziali meno frequentemente mantenendo le transazioni sicure.

>[!NOTE]
>
>I flussi di lavoro SSO fanno parte del pacchetto Premium Workflow. Per utilizzare questa funzionalità, contatta il tuo rappresentante commerciale Primetime .

## Stato attuale per SSO su varie piattaforme {#current-sso-status-platforms}

| Piattaforma/Dispositivo | Supporto SSO | Tipo SSO | Copertura MVPD | Note |
|:-------------------:|:-----------:|:---------------------------------------:|-----------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Web (JavaScript) | Sì | Token di autenticazione condivisa (Adobe SSO) | Tutto | Nessun SSO cross-browser Segui le istruzioni contenute nella Guida all&#39;integrazione del programmatore per JavaScript. Dopo aver seguito le istruzioni, SSO è abilitato per impostazione predefinita.  L&#39;abilitazione dell&#39;autenticazione per il richiedente interrompe l&#39;SSO |
| iOS | Sì | SSO piattaforma - scambio token | A seconda del supporto di Apple, l’elenco è disponibile qui | Da iOS 10, Apple &amp; Adobe ha introdotto la funzionalità SSO per i programmatori partecipanti e gli MVPD. Utilizzando l’SDK iOS di Adobe più recente o l’API REST Clientless di Adobe e implementando la funzionalità SSO di Apple puoi trarre vantaggio dall’SSO sui dispositivi iOS. Maggiori dettagli sull&#39;implementazione dell&#39;SDK sono disponibili qui e maggiori dettagli sull&#39;implementazione senza client. Note aggiuntive: - Se non desideri utilizzare Apple SSO puoi comunque disporre di un SSO limitato tra app dello stesso fornitore (stesso ID bundle) che possono condividere l&#39;archiviazione e un ID (IDFV), in modo che SSO sia limitato solo alle app dello stesso fornitore. |
| Android | Sì | Token di autenticazione condivisa (Adobe SSO) | Tutto | Se l&#39;utente non accetta la richiesta di autorizzazione WRITE_EXTERNAL_STORAGE, la libreria utilizzerà un archivio locale in sandbox. L&#39;implicazione in questo caso è che non ci sarà SSO tra applicazioni diverse quando si utilizza lo storage locale. |
| tvOS - nuovo Apple TV | Sì | SSO piattaforma - scambio token | A seconda del supporto di Apple, l’elenco è disponibile qui | Da tvOS 10, Apple &amp; Adobe ha introdotto la funzionalità SSO per i programmatori partecipanti e MVPD. Utilizzando l&#39;SDK tvOS di Adobe più recente o utilizzando l&#39;API REST senza client di Adobe e implementando la funzionalità SSO di Apple puoi trarre vantaggio dall&#39;SSO sui dispositivi tvOS. Maggiori dettagli su tvOS SDK: qui e qui trovi ulteriori dettagli sull’implementazione senza client. |
| Roku | Sì | Token di autenticazione condivisa (Adobe SSO) | Elenco completo di copertura significativo da fornire a breve. | Roku SSO funziona preconfigurato con l&#39;API Clientless per tutti i clienti che rispettano le linee guida Roku, nessuna implementazione speciale richiesta. L&#39;SSO si basa sulle informazioni di identificazione del dispositivo che Roku invia in modo sicuro ad Adobe. |
| Amazon FireTV | Sì | Token di autenticazione condivisa (Adobe SSO) | Elenco completo di copertura significativo da fornire a breve. | FireTV SDK fornisce il supporto per Single Sign-On in base alle funzionalità Android. L&#39;SSO su questa piattaforma è possibile solo tra le app che per il momento utilizzano Adobe FireTV SDK. Maggiori informazioni sul nuovo SDK FireTV qui. Le app FireTV implementate su Clientless API potranno beneficiare di SSO entro il 2018. |
| Xbox 360 | No |  |  | Non è disponibile alcun ID dispositivo che possiamo sfruttare. È presente un App ID, quindi gli utenti non devono eseguire l&#39;autenticazione ogni volta. |
| Xbox One | No |  |  | Non è disponibile alcun ID dispositivo che possiamo sfruttare. È presente un App ID, quindi gli utenti non devono eseguire l&#39;autenticazione ogni volta. |
| Windows 8/10 | No |  |  | Non è disponibile alcun ID dispositivo che possiamo sfruttare. È presente un App ID, quindi gli utenti non devono eseguire l&#39;autenticazione ogni volta. |
| Samsung TV | No |  |  | Non è disponibile alcun ID dispositivo che possiamo sfruttare. È presente un App ID, quindi gli utenti non devono eseguire l&#39;autenticazione ogni volta. |

### Note su Xbox 360 e Xbox One {#notes-xbox-360}

* **Xbox 360**- Xbox 360 si basa sul servizio Live per fornire il token che incorpora il deviceID. I livelli del servizio Live nel valore appID per deviceID, che lo rendono ambito solo per l&#39;app. Per Xbox 360, Microsoft ha fornito ad Adobe una libreria Java per facilitare l&#39;analisi del token.

* **Xbox One**- Verrà emesso un token web JSON crittografato con il cert/key dell’editore e firmato da Microsoft. L&#39;Adobe estrae l&#39;ID dispositivo da un parametro chiamato DPI (Device Pairwise ID), diverso dal parametro Xbox 360 PDID (Partner Device ID). Il PDID esiste anche in Xbox One ma deve essere sostituito da questo nuovo parametro &quot;Device Pairwise ID&quot; (DPI).


### Disabilitazione dell&#39;SSO {#disable-sso}

In alcune situazioni alcune app o siti vorranno disabilitare SSO per soddisfare casi aziendali avanzati.

* **Per JS e SDK nativi** - Il team di supporto per l&#39;autenticazione Primetime può disabilitare SSO per una coppia Requestor ID/MVPD. Non è necessario alcun lavoro sui siti o nelle app native.  Una volta che l&#39;SSO è disabilitato dal team di supporto per l&#39;autenticazione di Primetime, le autenticazioni eseguite utilizzando la coppia RequestorId/MVPD specificata non saranno condivise con siti o app che utilizzano ID Requestor diversi. Inoltre, le autenticazioni esistenti con ID richiedenti diversi non saranno valide per la combinazione ID richiedente/MVPD in cui SSO è stato disabilitato. Tecnicamente, la disattivazione SSO viene eseguita mediante il binding del token AuthN alla specifica combinazione Requestor ID/MVPD.
* **Per API senza client** - È possibile disabilitare SSO nel flusso di autenticazione Clientless specificando un parametro appId non vuoto nelle chiamate REST. Puoi utilizzare qualsiasi stringa come valore, purché tale stringa sia univoca per l’ID richiedente. Tieni presente che per l’API Clientless, il programmatore/implementatore deve modificare il sito o l’app per aggiungere questo parametro specifico del richiedente.

>[!IMPORTANT]
>
>NOTA IMPORTANTE PER L&#39;API CLIENTLESS SSO: Alcuni MVPD richiedono che ogni rete (requestor ID) esegua il proprio flusso di autenticazione. Per i flussi basati sull’SDK (iOS, ecc.), questo viene gestito automaticamente dall’SDK. Tuttavia, per le API senza client questo deve essere gestito dal programmatore. A questo punto consigliamo vivamente ai programmatori di non abilitare i flussi SSO per le API Clientless e di utilizzare invece una combinazione di ID dispositivo + ID app per l’ID dispositivo. Adobe lavorerà anche al miglioramento dei flussi API Clientless in modo che sia possibile stabilire un SSO appropriato.

### Logout {#logout-sso-support}

I programmatori devono essere consapevoli che l&#39;azione &quot;Logout&quot; nel contesto del Single Sign-On, quando viene eseguita in un&#39;app/su un sito, eliminerà tutti i token sul dispositivo e l&#39;utente verrà disconnesso tra app/siti.

Se le condizioni SSO sono soddisfatte (sia che l&#39;SSO sia abilitato o disattivato), verrà eseguito lo Logout e tutte le informazioni di autenticazione e autorizzazione verranno eliminate.
