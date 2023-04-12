---
title: Registrazione dell'applicazione Android
description: Registrazione dell'applicazione Android
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---



# Registrazione dell&#39;applicazione Android {#android-application-registration}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#intro}

A partire dalla versione 3.0 dell’SDK di Android AccessEnabler, stiamo modificando il meccanismo di autenticazione con i server di Adobe. Invece di utilizzare una chiave pubblica e un sistema segreto per firmare il requestorID, stiamo introducendo il concetto di una stringa di istruzione Software che può essere utilizzata per ottenere un token di accesso che viene successivamente utilizzato per tutte le chiamate che l’SDK effettua ai nostri server. Oltre a un&#39;istruzione software, sarà necessario creare un collegamento profondo per l&#39;applicazione.

Per ulteriori informazioni, consulta [Registrazione client dinamica](/help/authentication/dynamic-client-registration.md)

## Cos&#39;è un&#39;istruzione software? {#what}

Un&#39;istruzione software è un token JWT che contiene informazioni sull&#39;applicazione. Ogni applicazione deve avere un&#39;istruzione software unica che viene utilizzata dai nostri server per identificare l&#39;applicazione nel sistema di Adobe. L&#39;istruzione software deve essere passata quando si inizializza l&#39;SDK di AccessEnabler e verrà utilizzata per registrare l&#39;applicazione con Adobe. Al momento della registrazione, l’SDK riceverà un ID client e un segreto client che verranno utilizzati per ottenere un token di accesso. Qualsiasi chiamata effettuata dall&#39;SDK ai nostri server richiederà un token di accesso valido. L’SDK è responsabile della registrazione dell’applicazione, del recupero e dell’aggiornamento del token di accesso.

>[!NOTE]
>
>Le istruzioni software sono specifiche per l&#39;app e non possono essere utilizzate per più applicazioni. Le istruzioni software a livello di programmatore hanno lo stesso vincolo, possono essere utilizzate solo per una singola applicazione, sia a canale singolo che a più canali.

## Come ottenere una dichiarazione software? {#how-to-get-ss}

### Se disponi dell&#39;accesso al dashboard TVE di Adobe:

* Apri il browser e passa a [Dashboard TVE di Adobe Primetime](https://console.auth.adobe.com).
* Passa a `Channels` e seleziona il canale.
* Passa a `Registered Applications` Tab.
* Fai clic su `Add new application`.
* Fornisci un nome e una versione per la tua applicazione e seleziona le piattaforme sulle quali sarà disponibile. Android nel nostro caso.
* Fornisci un nome di dominio scegliendo da un elenco di domini già configurati per il tuo programmatore.
* Invia le modifiche al server e quindi torna alla scheda Applicazioni registrate del canale.
* Dovresti visualizzare un elenco con tutte le applicazioni registrate. Seleziona la **Scarica** sull&#39;applicazione appena creata. Potrebbe essere necessario attendere alcuni minuti prima che l&#39;Informativa software sia pronta per il download.
* Verrà scaricato un file di testo. Utilizzare i relativi contenuti come dichiarazione software.

Per ulteriori informazioni, consulta [Gestione dinamica della registrazione client](/help/authentication/dynamic-client-registration-management.md)

### Se non disponi dell&#39;accesso al dashboard TVE di Adobe:

Invia un biglietto a `tve-support@adobe.com`. Includi tutte le informazioni necessarie come il canale, il nome dell&#39;applicazione, la versione e le piattaforme e qualcuno del nostro team di supporto creerà una dichiarazione software per te.

## Come utilizzare l&#39;istruzione software? {#how-to-use-ss}

Dopo aver ottenuto la dichiarazione software è necessario trasmetterla come parlamentare nel costruttore di Access Enabler. Si consiglia di ospitare l&#39;Informativa software in una posizione remota. In questo modo, è possibile revocare e modificare facilmente l&#39;Informativa software senza rilasciare una nuova versione dell&#39;applicazione.

## Creare e utilizzare un collegamento profondo per la tua applicazione {#create}

Su Android, utilizzare come valore di collegamento profondo l&#39;inverso del nome di dominio selezionato al momento della creazione dell&#39;istruzione software

Il collegamento profondo creato deve avere un valore univoco sul dispositivo Android. Quando più applicazioni utilizzano lo stesso valore di collegamento profondo, i flussi di autenticazione e logout interferiranno.

## Come utilizzare l&#39;istruzione software e il collegamento profondo {#use-both}

Nel file delle risorse dell&#39;applicazione `strings.xml` aggiungi il seguente codice:

```JAVA
    <string name="software_statement">softwarestatement value</string>
    <string name="redirect_uri">com.domain_name</string>
```

