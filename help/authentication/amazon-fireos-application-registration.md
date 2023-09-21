---
title: Registrazione applicazione Amazon FireOS
description: Registrazione applicazione Amazon FireOS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Registrazione applicazione Amazon FireOS {#amazon-fireos-application-registration}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Introduzione {#intro}

A partire dalla versione 3.0 dell’SDK di FireOS AccessEnabler, stiamo modificando il meccanismo di autenticazione con i server di Adobe. Invece di utilizzare una chiave pubblica e un sistema segreto per firmare l’ID richiedente, introduciamo il concetto di stringa di informativa software che può essere utilizzata per ottenere un token di accesso che viene successivamente utilizzato per tutte le chiamate dell’SDK ai nostri server. Oltre a una dichiarazione software, è necessario creare un collegamento profondo per l&#39;applicazione.

Per ulteriori informazioni, consulta [Registrazione client dinamici](/help/authentication/dynamic-client-registration.md)

## Che cos&#39;è una dichiarazione software? {#what}

Un rendiconto software è un token JWT che contiene informazioni sull’applicazione. Ogni applicazione deve disporre di una dichiarazione software univoca utilizzata dai nostri server per identificare l&#39;applicazione nel sistema Adobe. L&#39;istruzione software deve essere passata quando si inizializza l&#39;SDK di AccessEnabler e verrà utilizzata per registrare l&#39;applicazione con Adobe. Al momento della registrazione, l’SDK riceverà un ID client e un segreto client che verranno utilizzati per ottenere un token di accesso. Qualsiasi chiamata effettuata dall&#39;SDK ai nostri server richiederà un token di accesso valido. L’SDK è responsabile della registrazione dell’applicazione, del recupero e dell’aggiornamento del token di accesso.

**Nota:** Le istruzioni software sono specifiche dell&#39;app e non possono essere utilizzate per più di un&#39;applicazione. Tieni presente che questo vale anche per le applicazioni che offrono accesso a più canali.

## Come si ottiene una dichiarazione software? {#how-to}

### Se hai accesso al dashboard TVE di Adobe:

- Apri il browser e passa a <https://console.auth.adobe.com>
- Accedi a `Channels` e selezionare il canale.
- Accedi a `Registered Applications` Tab.
- Fai clic su `Add new application`.
- Specifica un nome e una versione per l’applicazione e seleziona le piattaforme su cui sarà disponibile (ad esempio, Android nel nostro caso).
- Specifica un nome dominio scegliendo un dominio da un elenco già configurato per il programmatore.
- Invia le modifiche al server e quindi torna alla scheda Applicazioni registrate del canale.
- Dovresti visualizzare un elenco con tutte le applicazioni registrate. Fai clic su `Download` sull&#39;applicazione appena creata. Nota: potrebbe essere necessario attendere alcuni minuti prima che l&#39;informativa software sia pronta per il download.
- Verrà scaricato un file di testo. Utilizza il contenuto come informativa sul software.

Per ulteriori informazioni, consulta [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)

### Se non hai accesso al dashboard TVE di Adobe:

Invia un ticket a <tve-support@adobe.com>. Includere tutte le informazioni necessarie, inclusi il canale, il nome dell&#39;applicazione, la versione e le piattaforme. Verrà creata una dichiarazione software per l&#39;utente da parte del team di supporto.

## Come utilizzare la dichiarazione software? {#use}

Dopo aver ottenuto l&#39;Informativa sul software, è necessario trasmetterla come parametro nel costruttore di Access Enabler. Si consiglia di ospitare l&#39;Informativa sul software in una posizione remota. In questo modo, è possibile revocare e modificare facilmente l&#39;Informativa software senza rilasciare una nuova versione dell&#39;applicazione.

## Come utilizzare l&#39;Informativa sul software {#use-both}

Nel file di risorse dell’applicazione `strings.xml` aggiungi il seguente codice:

```XML
<string name="software_statement">softwarestatement value</string>
```
