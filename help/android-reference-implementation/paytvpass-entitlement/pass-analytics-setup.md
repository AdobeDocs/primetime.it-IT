---
description: Potete impostare l'implementazione di riferimento per utilizzare  rapporto Adobe Analytics.
seo-description: Potete impostare l'implementazione di riferimento per utilizzare  rapporto Adobe Analytics.
seo-title: Configurare  rapporti Adobe Analytics
title: Configurare  rapporti Adobe Analytics
uuid: bdf8bb7f-a0c8-48a2-a632-0b872687f3fe
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Configurare  Adobe Analytics Reporting {#configure-adobe-analytics-reporting}

Potete impostare l&#39;implementazione di riferimento per utilizzare  rapporto Adobe Analytics.

L&#39;implementazione di riferimento è configurata per inviare i dati dell&#39;evento di autenticazione Primetime ad  Adobe Analytics tramite la libreria mobile  Adobe inclusa nell&#39;SDK di Primetime. Per abilitare e utilizzare i dati dell&#39;evento inviati dall&#39;applicazione, è innanzitutto necessario creare un account Adobe Analytics . Una volta creato l&#39;account:

1. Configurate l’applicazione con le informazioni sull’account; e
1. Create delle regole di elaborazione per personalizzare il modo in cui i dati dell&#39;evento vengono visualizzati nei rapporti.

La tabella seguente presenta i dati inviati a  Adobe Analytics:

| Nome azione | `a.media.pass.event.MvpdSelection` | L&#39;utente ha selezionato un filtro di programmazione video multi-canale (MVPD) in una finestra di dialogo di selezione |
|---|---|---|
| Dati contestuali | `a.media.pass.MvpdId (String)` | MVPD selezionato dall&#39;utente |
|  | `a.media.pass.ClientType` | (String) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |
|  |  |  |
| Nome azione | `a.media.pass.event.AuthenticationDetection` | Flusso di lavoro di autenticazione completato |
| Dati contestuali | `a.media.pass.Successful` | (Booleano) Se la richiesta del token è riuscita, true o false |
|  | `a.media.pass.MvpdId` | (Stringa) MVPD selezionato dall&#39;utente |
|  | `a.media.pass.Guid` | (Stringa) Un ID di tracciamento |
|  | `a.media.pass.Cached` | (Booleano) Token già presente nella cache, true o false |
|  | `a.media.pass.ClientType` | (String) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |
|  |  |  |
| Nome azione | `a.media.pass.event.AuthorizationDetection` | Flusso di lavoro di autorizzazione completato |
| Dati contestuali | `a.media.pass.Successful` | (Booleano) Se la richiesta del token è riuscita, true o false |
|  | `a.media.pass.MvpdId` | (Stringa) L&#39;utente ha selezionato MVPD |
|  | `a.media.pass.Guid` | (Stringa) Un ID di tracciamento |
|  | `a.media.pass.Cached` | (Booleano) Token già presente nella cache, true o false |
|  | `a.media.pass.Error` | (Stringa) L&#39;errore se il tentativo di autorizzazione non è riuscito |
|  | `a.media.pass.ErrorDetails` | (String) Ulteriori dettagli sull&#39;errore |
|  | `a.media.pass.ClientType` | (String) Il tipo di client è &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |

1. Configurate l&#39;applicazione per l&#39;utilizzo con Adobe Marketing Cloud.

   Per abilitare l&#39;invio di dati di autenticazione Primetime ad  Adobe Analytics, è necessario aggiungere un file di configurazione [!DNL `ADBMobileConfig.json`] all&#39;implementazione di riferimento in fase di compilazione. Si tratta esattamente dello stesso file di configurazione utilizzato dall’SDK Primetime per inviare i dati di Video Analytics al Marketing Cloud. Per ulteriori informazioni sulla configurazione di un&#39;applicazione con l&#39;account Adobe Analytics , consultare la [documentazione Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/).
1. Creare le regole di elaborazione.

   I dati dell&#39;evento di autenticazione Primetime inviati dall&#39;implementazione di riferimento non verranno visualizzati automaticamente nei report di analisi. È innanzitutto necessario utilizzare i dati mediante la creazione di regole di elaborazione. Consultare la [ documentazione Adobe Analytics sulla creazione di regole di elaborazione](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
