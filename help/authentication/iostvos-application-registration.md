---
title: Registrazione dell'applicazione iOS/tvOS
description: Registrazione dell'applicazione iOS/tvOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Registrazione dell&#39;applicazione iOS/tvOS {#iostvos-application-registration}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#Intro}

A partire dalla versione 3.0 dell’SDK iOS/tvOS AccessEnabler, stiamo modificando il meccanismo di autenticazione con i server Adobe. Invece di utilizzare una chiave pubblica e un sistema segreto per firmare il requestorID, stiamo introducendo il concetto di una stringa di istruzione Software che può essere utilizzata per ottenere un token di accesso che viene successivamente utilizzato per tutte le chiamate che l’SDK effettua ai nostri server. Oltre a un&#39;istruzione software, sarà necessario anche uno schema URL personalizzato per la tua applicazione.

Per ulteriori informazioni, consulta [Registrazione client dinamica](/help/authentication/dynamic-client-registration.md)

## Cos&#39;è un&#39;istruzione software? {#Soft_state}

Un&#39;istruzione software è un token JWT che contiene informazioni sull&#39;applicazione. Ogni applicazione deve avere un&#39;istruzione software unica che viene utilizzata dai nostri server per identificare l&#39;applicazione nel sistema di Adobe. L&#39;istruzione software deve essere passata quando si inizializza l&#39;SDK di AccessEnabler e verrà utilizzata per registrare l&#39;applicazione con Adobe. Al momento della registrazione, l’SDK riceverà un ID client e un segreto client che verranno utilizzati per ottenere un token di accesso. Qualsiasi chiamata effettuata dall&#39;SDK ai nostri server richiederà un token di accesso valido. L’SDK è responsabile della registrazione dell’applicazione, del recupero e dell’aggiornamento del token di accesso.

**Nota:** Un&#39;istruzione software è specifica per l&#39;app e la stessa istruzione software non può essere utilizzata su più di un&#39;applicazione. Le istruzioni software a livello di programmatore seguono le stesse, ovvero possono essere utilizzate solo per applicazioni singole, sia per canale singolo che per multicanale. Questa limitazione si applica anche allo schema personalizzato.

## Come ottenere una dichiarazione software? {#obtain}

### Se disponi dell&#39;accesso al dashboard TVE di Adobe:

- Apri il browser e passa a <https://console.auth.adobe.com>
- Passa a `Channels` e seleziona il canale.
- Passa a `Registered Applications` Tab.
- Fai clic su `Add new application`.
- Fornisci un nome e una versione per la tua applicazione e seleziona le piattaforme sulle quali sarà disponibile. iOS/tvOS nel nostro caso.
- Invia le modifiche al server e quindi torna alla scheda Applicazioni registrate del canale.
- Dovresti visualizzare un elenco con tutte le applicazioni registrate. Fai clic sul pulsante   `Download` sull&#39;applicazione appena creata. Potrebbe essere necessario attendere alcuni minuti prima che l&#39;Informativa software sia pronta per il download.
- Verrà scaricato un file di testo. Utilizzare i contenuti come dichiarazione software.

Per ulteriori informazioni, consulta [Gestione dinamica della registrazione client](/help/authentication/dynamic-client-registration-management.md).

### Se non disponi dell&#39;accesso al dashboard TVE di Adobe:

Invia un biglietto a <tve-support@adobe.com>. Includi tutte le informazioni necessarie, come il canale, il nome dell&#39;applicazione, la versione e le piattaforme, e qualcuno del nostro team di supporto creerà una dichiarazione software per te.

## Come utilizzare l&#39;istruzione software? {#use}

Dopo aver ottenuto la dichiarazione software è necessario trasmetterla come parlamentare nel costruttore di Access Enabler. Si consiglia di ospitare l&#39;Informativa software in una posizione remota. In questo modo, è possibile revocare e modificare facilmente l&#39;Informativa software senza rilasciare una nuova versione dell&#39;applicazione.

## Generazione di uno schema URL personalizzato per l&#39;applicazione {#generating}

### Se disponi dell&#39;accesso al dashboard TVE di Adobe:

- Apri il browser e passa a <https://console.auth.adobe.com>
- Passa a `Channels` e seleziona il canale.
- Passa a `Custom Schemes` Tab.
- Fai clic su `Generate a new custom scheme`.
- Verrà generato un nuovo schema personalizzato per l&#39;applicazione. Ex: `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- Invia le modifiche al server.

### Se non disponi dell&#39;accesso al dashboard TVE di Adobe:

Invia un biglietto a <tve-support@adobe.com>. Includi l’ID canale e qualcuno del nostro team di supporto creerà uno schema personalizzato per te.

## Come utilizzare lo schema personalizzato {#use_custom}

Nella tua applicazione `info.plist` aggiungi il seguente codice:

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>adbe.u-XFXJeTSDuJiIQs0HVRAg</string> // replace this with your custom scheme
            </array>
        </dict>
    </array>
```
