---
title: Limitazioni dell’SDK JS per il browser Safari
description: Limitazioni dell’SDK JS per il browser Safari
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# Limitazioni dell’SDK JS per il browser Safari {#js-sdk-limitations-for-safari-browser}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

<!--
>[!IMPORTANT] 
>
>We are strongly recommending [migration to AccessEnabler JavaScript SDK versions 4.x](http://tve.helpdocsonline.com/accessenabler-js-v4-migration-guide) in order to have a stable and predictable behavior on Safari browser.-->


## Safari 10 {#safari10}

**Dettagli**

* A partire da Safari 10, le impostazioni di privacy predefinite del browser smetteranno di funzionare le funzioni di autenticazione Single Sign-On (SSO), Single Logout (SLO) e passive. L&#39;autenticazione Single Sign-On (SSO) e passiva non funzionerà nemmeno nella stessa sessione tra più schede o finestre del browser.

* Queste modifiche influiscono sui processi di autenticazione di Adobe Primetime e hanno un impatto sui processi di SDK JavaScript di AccessEnabler per le seguenti versioni: v2 (versioni 2.x), v3 (versioni 3.x), v4 (versioni 4.x).

### Mitigazione {#mitigation-safari10}

* Per attenuare queste limitazioni, puoi dare istruzioni all’utente di modificare le impostazioni della privacy del browser Safari 10 e utilizzare il &quot;**Consenti sempre**&quot; opzione per &quot;**Cookie e dati del sito web**&quot; voce nella scheda Privacy del browser da Preferenze, come illustrato di seguito.

   ![](assets/always-allow-safari10.png)


## Safari 11 {#safari11}

**Dettagli**

>[!IMPORTANT]
>
>Tutti i dettagli di cui sopra della sezione Safari 10 si applicano ancora nel caso di Safari 11.

* A partire da Safari 11, il browser introduce [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/)Meccanismo (ITP), una tecnologia che utilizza l’euristica per impedire il tracciamento intersito. Queste caratteristiche influiscono sul modo in cui i cookie di terze parti vengono memorizzati e riprodotti sulle chiamate di rete, il che significa che, a seconda dell’attivazione del meccanismo ITP, il browser Safari blocca i cookie di terze parti nella comunicazione client-modello server.

* Il servizio di autenticazione di Adobe Primetime utilizza e si basa sui cookie come parte del processo di autenticazione **per funzionare**. In situazioni in cui il processo di autenticazione avviene automaticamente (ad esempio, Temp Pass) o in implementazioni che utilizzano funzionalità iFrames o &quot;senza aggiornamenti&quot;, i cookie di Adobe sono considerati cookie di terze parti e bloccati per impostazione predefinita. Per tutti gli altri casi, Safari utilizza un algoritmo di apprendimento automatico che potrebbe contrassegnare tutti i cookie del servizio di autenticazione Primetime di Adobe come cookie di tracciamento, essendo pertanto soggetto al blocco di ITP.  

* In conclusione, un utente del browser Safari 11 potrebbe non essere in grado di eseguire l’autenticazione su un sito web abilitato per l’autenticazione Adobe Primetime dopo l’attivazione del meccanismo ITP (Intelligent Tracking Prevention), soprattutto quando gli utenti utilizzano più siti web abilitati per l’autenticazione di Primethime Adobe. Pertanto, l’esperienza di autenticazione dell’utente potrebbe essere inaspettata e non definita, che va dall’impossibilità di accedere, a una durata di autenticazione inferiore a quella prevista.

* Queste modifiche influiscono sui processi di autenticazione Adobe Primetime delle seguenti versioni dell&#39;SDK JavaScript di AccessEnabler e hanno un impatto su di essi: v2 (versioni 2.x), v3 (versioni 3.x).

### Mitigazione {#mitigation-safari11}

* Per AccessEnabler JavaScript SDK v3 (versioni 3.x) e AccessEnabler JavaScript SDK v4 (versioni 4.x), la libreria contiene un meccanismo in grado di identificare le situazioni in cui l&#39;autenticazione dell&#39;utente è stata bloccata a causa della mancanza di cookie richiesti. In queste situazioni la libreria attiva un callback di errore specifico [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference), che viene ritrasmesso al sito web abilitato per l’autenticazione di Adobe Primetime al fine di essere utilizzato come segnale per indicare all’utente di intraprendere azioni che possono mitigare il problema. Per beneficiare di tale meccanismo, il sito web deve [Segnalazione errori](/help/authentication/error-reporting.md) specifica.

* Per AccessEnabler JavaScript SDK v2 (versioni 2.x), la libreria non offre il meccanismo descritto sopra, pertanto il sito web abilitato per l&#39;autenticazione di Adobe Primetime non può essere segnalato quando istruire l&#39;utente ad adottare misure per mitigare il problema.

* L&#39;elenco delle azioni che possono attenuare i problemi di cui sopra **si applica a tutte e tre le versioni** di AccessEnabler JavaScript SDK.

* Quando [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) il callback di errore viene ricevuto dal sito web dell’implementatore, l’utente deve essere informato della disattivazione di ITP (Intelligent Tracking Prevention) e dell’abilitazione dei cookie di terze parti da parte di:

* In caso di Mac OS X High Sierra e successivi: Deselezionando &quot;**Impedisci il tracciamento intersito**&quot; opzione per &quot;**Tracciamento dei siti web**&quot; voce nella scheda Privacy del browser da Preferenze, come illustrato di seguito.

   ![](assets/uncheck-prvnt-cr-st-tr-safari11.png)

* In caso di Mac OS X Sierra e precedenti: Controllo di &quot;**Consenti sempre**&quot; opzione per &quot;**Cookie e dati del sito web**&quot; voce nella scheda Privacy del browser da Preferenze, come illustrato di seguito.

   ![](assets/always-allow-safari11.png)

## Safari 12 {#safari12}

**Dettagli**

>[!IMPORTANT]
>
>Tutti i dettagli di cui sopra della sezione Safari 10 e della sezione Safari 11 si applicano ancora nel caso di Safari 12.

Questa sezione descrive i problemi di compatibilità di **AccessEnabler JavaScript SDK versioni 4.x** su Safari 12.

>[!NOTE]
>
>Tieni presente che nel caso di AccessEnabler JavaScript SDK versione 2.x e AccessEnabler JavaScript SDK versione 3.x, entrambi utilizzano cookie di terze parti per i processi di autenticazione e a causa dei criteri ITP e di cookie di terze parti che iniziano con Safari 11, l’esperienza di autenticazione dell’utente potrebbe essere inaspettata e non definita, che vanno dall’impossibilità di accedere a una durata di autenticazione inferiore al previsto.


### Funzionalità certificata di AccessEnabler JavaScript SDK v4 (versioni 4.x) su Safari 12 {#certified-functionality-of-accessenabler-javacscript=sdk-v4}

* **Autenticazione** i flussi che utilizzano l’interazione con l’utente funzioneranno sempre, anche se il browser dell’utente ha cookie di terze parti disabilitati, perché a partire dalla versione 4.0 l’SDK JavaScript di AccessEnabler non utilizza più cookie di terze parti per i processi di autenticazione.

>[!NOTE]
>
>L&#39;utente DEVE interagire con il sito per aprire le pagine di accesso e/o interagire con la pagina di accesso MVPD.

* **Metadati di autorizzazione/verifica preliminare/utente** le operazioni sono completamente funzionanti, purché l&#39;utente sia già autenticato.

### Problemi noti di AccessEnabler JavaScript SDK v4 (versioni 4.x) su Safari 12 {#known-issues-of-accessenabler-javascript-sdk-4}

* SSO e SLO

   * A causa della modalità di implementazione di localStorage in Safari a partire da Safari 10, l’SDK JS non può più condividere lo stato di accesso tramite un iFrame di dominio comune. Questo significa che l&#39;utente deve effettuare l&#39;accesso a ogni sito che utilizza AccessEnabler JavaScript SDK. La disconnessione non elimina anche i token di autenticazione tra siti diversi, pertanto l’utente deve disconnettersi da ciascun sito web abilitato per l’autenticazione di Adobe Primetime.

* Passaggio Temp

   * Per le passate temporanee, l&#39;SDK JavaScript di AccessEnabler utilizza un meccanismo di individualizzazione, per bloccare un token di autenticazione a un dispositivo specifico (istanza del browser). A causa dei nuovi meccanismi in Safari 12 progettati per impedire il tracciamento, l&#39;impronta digitale che stiamo elaborando e utilizzando nel meccanismo di individualizzazione **sarà lo stesso per tutti gli utenti che hanno lo stesso indirizzo IP**. Consideriamo l’IP client a scopo di individualizzazione, ma anche così l’impatto è sugli utenti che condividono lo stesso indirizzo IP pubblico. Per questi utenti, calcoleremo lo stesso id di individualizzazione e il pass temporaneo sarà legato ad esso. Ciò significa che una volta che un utente utilizza un pass temporaneo, nessun altro avrà accesso ad esso \! Questo ha un impatto in particolare sugli utenti aziendali, gli istituti di istruzione o qualsiasi altra organizzazione che hanno più utenti che utilizzano NAT o un proxy comune per accedere a Internet.

>[!NOTE]
>
>Questo problema interessa gli utenti solo se l&#39;implementatore utilizza Temp Pass a seguito dell&#39;interazione dell&#39;utente, altrimenti l&#39;autenticazione Temp Pass è soggetta a **Flussi automatici** sotto.

* Flussi automatici

   * I flussi di autenticazione tentati in una modalità automatizzata, senza alcuna interazione con l’utente non avranno esito positivo in Safari 12 quando si utilizza JS SDK 4.0. Tieni presente che l’imminente SDK 4.1 per JS risolve tutti i problemi relativi ai flussi automatizzati.

Casi di utilizzo interessati da questo problema:

* Autenticazione automatica TempPass (anteprima gratuita) - per tali flussi, l&#39;SDK genererà un errore N130.

* Autenticazione passiva (errore silenzioso) - all&#39;utente viene richiesto di selezionare questo MVPD e di immettere le credenziali

### Mitigazione {#mitigation-safari12}

**SSO e SLO**

Al momento di questa scrittura non è disponibile né possibile alcuna mitigazione nota. Apple ha introdotto un’&quot;API di accesso allo storage&quot; in Safari 12 (`https://webkit.org/blog/8124/introducing-storage-access-api`), ma l&#39;implementazione corrente non si applica a localStorage ma solo ai cookie. Inoltre, l’API richiede l’interazione dell’utente per poter essere utilizzata e, una volta utilizzata, all’utente viene richiesta una finestra di dialogo di autorizzazione simile a quella riportata di seguito.

![](assets/permission-dialog-apple.png)


A questo punto questi requisiti/prompt di Safari non sono allineati ai nostri requisiti UX e non abbiamo un comportamento coerente come su altri browser, dove SSO &quot;funziona&quot; solo una volta salvato un token in un dominio comune localStorage.

**Passaggio Temp**

Per attenuare i problemi di individualizzazione e per avere un&#39;interazione con l&#39;utente ti consigliamo di utilizzare **[Passaggio temporaneo promozionale ](/help/authentication/promotional-temp-pass.md)** In modo interattivo e fornisci almeno un’informazione aggiuntiva sull’utente (ad esempio l’indirizzo e-mail).

## Safari 13 {#safari13}

**Dettagli**

>[!IMPORTANT]
>
>Tutti i dettagli di cui sopra della sezione Safari 10 fino alla sezione Safari 12 ancora applicabili nel caso di Safari 13.


A partire da Safari 13, il browser introduce nuove modifiche al [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP), per impedire il tracciamento intersito, rendere le caratteristiche del meccanismo più rigorose nel processo di segnalazione dei cookie di terze parti come cookie di tracciamento.

Come descritto nelle sezioni precedenti, il servizio di autenticazione Adobe Primetime utilizza e si basa sui cookie di terze parti come parte dei processi di autenticazione quando le implementazioni utilizzano l&#39;SDK JavaScript di AccessEnabler v2 (versioni 2.x) e l&#39;SDK JavaScript di AccessEnabler v3 (versioni 3.x). Rispetto alle versioni precedenti del browser Safari quando ITP ha passato un po’ di tempo a &quot;imparare&quot; sull’interazione tra l’utente e le parti interessate (siti web del programmatore e Adobe), il browser Safari 13 blocca i cookie di terze parti iniziali, considerati cookie di tracciamento nella comunicazione client-modello server.

In conclusione, un utente del browser Safari 13 probabilmente non sarà in grado di avviare nuove autenticazioni su un sito web abilitato per l’autenticazione di Adobe Primetime che utilizza una versione precedente di AccessEnabler JavaScript SDK, v2 (versioni 2.x) o v3 (versioni 3.x). Ciò si verifica a causa del fatto che tutti i cookie del servizio di autenticazione Primetime richiesti da Adobe sono bloccati da ITP, rendendo quindi il servizio incapace di soddisfare la richiesta di autenticazione.

La libreria SDK JavaScript di AccessEnabler v4 (versioni 4.x) non utilizza cookie di terze parti per il processo di autenticazione, pertanto le sue operazioni non sono influenzate in alcun modo dalle modifiche di Safari 13.

### Mitigazione {#mitigation-safari13}

Prima di tutto raccomandiamo con forza **migrazione alle versioni SDK 4.x di AccessEnabler JavaScript** per avere un comportamento stabile e prevedibile sul browser Safari.

In secondo luogo, per AccessEnabler JavaScript SDK v3 (versioni 3.x), la libreria contiene un meccanismo in grado di identificare le situazioni in cui l&#39;autenticazione degli utenti è stata bloccata a causa della mancanza di cookie richiesti. In queste situazioni la libreria attiva un callback di errore specifico ([N130](/help/authentication/error-reporting.md#advanced-error-codes-reference)), che viene ritrasmessa al sito web abilitato per l’autenticazione di Adobe Primetime al fine di essere utilizzata come segnale per indicare all’utente di intraprendere azioni che possono mitigare il problema. Per beneficiare di tale meccanismo, il sito web deve [Segnalazione errori](/help/authentication/error-reporting.md) specifica.

Per AccessEnabler JavaScript SDK v2 (versioni 2.x), la libreria non offre il meccanismo descritto sopra, pertanto il sito web abilitato per l&#39;autenticazione di Adobe Primetime non può essere segnalato quando istruire l&#39;utente ad adottare misure per mitigare il problema.

Quando [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) il callback di errore viene ricevuto dal sito web dell’implementatore, l’utente deve essere informato della disattivazione di ITP (Intelligent Tracking Prevention) e dell’abilitazione dei cookie di terze parti da parte di:

* In caso di Mac OS X High Sierra e successivi: Deselezionando &quot;**Impedisci il tracciamento intersito**&quot; opzione per &quot;**Tracciamento dei siti web**&quot; voce nella scheda Privacy del browser da Preferenze, come illustrato di seguito.

   ![](assets/prvnt-cross-site-tr-safari13.png)

* In caso di Mac OS X Sierra e precedenti: Controllo</span>&quot;**Consenti sempre**&quot; opzione per &quot;**Cookie e dati del sito web**&quot; voce nella scheda Privacy del browser da Preferenze, come illustrato di seguito.

   ![](assets/always-allow-safari13.png)

