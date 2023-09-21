---
description: Per utilizzare le funzioni di reporting di Adobe Analytics, puoi impostare l’implementazione di riferimento.
title: Configurare il reporting di Adobe Analytics
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Configurare il reporting di Adobe Analytics {#configure-adobe-analytics-reporting}

Per utilizzare le funzioni di reporting di Adobe Analytics, puoi impostare l’implementazione di riferimento.

L’implementazione di riferimento è configurata per inviare i dati dell’evento di autenticazione Primetime ad Adobe Analytics utilizzando la libreria mobile di Adobe inclusa nell’SDK di Primetime. Per abilitare e utilizzare i dati evento inviati dall’applicazione, devi innanzitutto creare un account Adobe Analytics. Una volta creato l’account:

1. Configurare l&#39;applicazione con le informazioni sull&#39;account; e
1. Crea regole di elaborazione per personalizzare la modalità di visualizzazione dei dati dell’evento nei rapporti.

La tabella seguente presenta i dati inviati ad Adobe Analytics:

| Nome azione | `a.media.pass.event.MvpdSelection` | L’utente ha selezionato un MVPD (Multi-Channel Video Programming Distributor) in una finestra di dialogo di selezione |
|---|---|---|
| Dati contestuali | `a.media.pass.MvpdId (String)` | MVPD selezionato dall&#39;utente |
|  | `a.media.pass.ClientType` | (Stringa) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |
|  | | |
| Nome azione | `a.media.pass.event.AuthenticationDetection` | Flusso di lavoro di autenticazione completato |
| Dati contestuali | `a.media.pass.Successful` | (Booleano) Indica se la richiesta del token è riuscita, true o false |
|  | `a.media.pass.MvpdId` | (Stringa) MVPD selezionato dall&#39;utente |
|  | `a.media.pass.Guid` | (Stringa) Un ID di tracciamento |
|  | `a.media.pass.Cached` | (Booleano) Token già nella cache, true o false |
|  | `a.media.pass.ClientType` | (Stringa) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |
|  | | |
| Nome azione | `a.media.pass.event.AuthorizationDetection` | Un flusso di lavoro di autorizzazione è stato completato |
| Dati contestuali | `a.media.pass.Successful` | (Booleano) Indica se la richiesta del token è riuscita, true o false |
|  | `a.media.pass.MvpdId` | (Stringa) MVPD selezionato dall&#39;utente |
|  | `a.media.pass.Guid` | (Stringa) Un ID di tracciamento |
|  | `a.media.pass.Cached` | (Booleano) Token già nella cache, true o false |
|  | `a.media.pass.Error` | (Stringa) L’errore se il tentativo di autorizzazione non è riuscito |
|  | `a.media.pass.ErrorDetails` | (Stringa) Ulteriori dettagli sull’errore |
|  | `a.media.pass.ClientType` | (Stringa) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |

1. Configura l’applicazione per l’utilizzo con Adobe Marketing Cloud.

   Per abilitare l’invio di dati di autenticazione Primetime Primetime ad Adobe Analytics, è necessario [!DNL `ADBMobileConfig.json`] Il file di configurazione deve essere aggiunto all’implementazione di riferimento in fase di compilazione. Si tratta esattamente dello stesso file di configurazione utilizzato dall’SDK Primetime per inviare dati di analisi video al Marketing Cloud. Consulta la sezione [Documentazione di Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/) per ulteriori informazioni sulla configurazione di un’applicazione con il tuo account Adobe Analytics.
1. Creare regole di elaborazione.

   I dati dell’evento di autenticazione Primetime inviati dall’implementazione di riferimento non verranno visualizzati automaticamente nei rapporti di analisi. Devi innanzitutto utilizzare i dati creando regole di elaborazione. Consulta la sezione [Documentazione di Adobe Analytics sulla creazione di regole di elaborazione](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
