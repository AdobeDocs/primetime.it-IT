---
description: Puoi impostare l’implementazione di riferimento per utilizzare i rapporti di Adobe Analytics.
title: Configurare i rapporti di Adobe Analytics
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# Configurare Adobe Analytics Reporting {#configure-adobe-analytics-reporting}

Puoi impostare l’implementazione di riferimento per utilizzare i rapporti di Adobe Analytics.

L’implementazione di riferimento è configurata per inviare dati evento di autenticazione di Primetime ad Adobe Analytics utilizzando la libreria mobile Adobe inclusa nell’SDK di Primetime. Per abilitare e utilizzare i dati dell’evento inviati dall’applicazione, devi innanzitutto creare un account Adobe Analytics. Una volta creato l’account:

1. Configura l&#39;applicazione con le informazioni sul tuo account; e
1. Crea regole di elaborazione per personalizzare la modalità di visualizzazione dei dati dell’evento all’interno dei rapporti.

La tabella seguente presenta i dati inviati ad Adobe Analytics:

| Nome azione | `a.media.pass.event.MvpdSelection` | L&#39;utente ha selezionato un attributo Multi-channel Video Programming Distirbutor (MVPD) in una finestra di dialogo di selezione |
|---|---|---|
| Dati contestuali | `a.media.pass.MvpdId (String)` | MVPD selezionato dall&#39;utente |
|  | `a.media.pass.ClientType` | (Stringa) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot;. |
|  |  |  |
| Nome azione | `a.media.pass.event.AuthenticationDetection` | Flusso di lavoro di autenticazione completato |
| Dati contestuali | `a.media.pass.Successful` | (Booleano) Se la richiesta del token è riuscita, true o false |
|  | `a.media.pass.MvpdId` | (Stringa) MVPD selezionato dall&#39;utente |
|  | `a.media.pass.Guid` | (Stringa) Un ID di tracciamento |
|  | `a.media.pass.Cached` | (Booleano) Token già presente nella cache, true o false |
|  | `a.media.pass.ClientType` | (Stringa) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot;. |
|  |  |  |
| Nome azione | `a.media.pass.event.AuthorizationDetection` | Flusso di lavoro di autorizzazione completato |
| Dati contestuali | `a.media.pass.Successful` | (Booleano) Se la richiesta del token è riuscita, true o false |
|  | `a.media.pass.MvpdId` | (Stringa) L&#39;utente ha selezionato MVPD |
|  | `a.media.pass.Guid` | (Stringa) Un ID di tracciamento |
|  | `a.media.pass.Cached` | (Booleano) Token già presente nella cache, true o false |
|  | `a.media.pass.Error` | (Stringa) L&#39;errore se il tentativo di autorizzazione non è riuscito |
|  | `a.media.pass.ErrorDetails` | (Stringa) Ulteriori dettagli sull&#39;errore |
|  | `a.media.pass.ClientType` | (Stringa) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot;. |

1. Configura l&#39;applicazione per l&#39;utilizzo con Adobe Marketing Cloud.

   Per abilitare l’invio di dati di autenticazione Primetime Primetime ad Adobe Analytics, è necessario aggiungere un file di configurazione [!DNL `ADBMobileConfig.json`] all’implementazione di riferimento in fase di compilazione. Si tratta esattamente dello stesso file di configurazione utilizzato dall’SDK Primetime per inviare i dati di Video Analytics al Marketing Cloud. Per ulteriori informazioni sulla configurazione di un&#39;applicazione con il tuo account Adobe Analytics, consulta la [documentazione Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/) .
1. Creare regole di elaborazione.

   I dati dell’evento di autenticazione Primetime inviati dall’implementazione di riferimento non verranno visualizzati automaticamente nei rapporti di analisi. È innanzitutto necessario utilizzare i dati creando regole di elaborazione. Consulta la documentazione [Adobe Analytics sulla creazione di regole di elaborazione](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
