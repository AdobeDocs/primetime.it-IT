---
title: Codici di errore BEES
description: Codici di errore BEES
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Codici di errore BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Se si verifica un errore durante un controllo BEES, viene visualizzata una `DRMErrorEvent` verrà restituito al client. Puoi analizzare le proprietà di questo evento per trovare dettagli sulla natura dell’errore. Di seguito è riportato un sottoinsieme di possibili codici di errore.

| Errore | Descrizione |
|---|---|
| `3304:305` | Errore generico di autorizzazione da parte di Primetime Cloud DRM durante il tentativo di gestire una richiesta di autenticazione/autorizzazione. In genere non è associato a un problema di tipo API. Se questo errore si verifica in modo costante, è necessario inviare un ticket di problema al team DRM di Primetime Cloud insieme alle informazioni di diagnostica. |
| `3329:0` | Errore specifico dell’applicazione (dall’autorizzatore BEES). Se non viene restituito alcun codice di errore secondario, nel testo dell’errore verranno visualizzati i dettagli del problema. Ad esempio, si è verificato un problema durante l’analisi della risposta o il server BEES non era raggiungibile. |
| `3329:<HTTP error code>` | Il server BEES ha emesso una risposta HTTP diversa da 200. Il codice di errore HTTP viene restituito al client nel campo del codice di errore secondario. Ciò potrebbe indicare un problema di configurazione o un’interruzione del server BEES. |
| `3329:<x>` | Il server BEES non ha consentito la richiesta di licenza. Il codice di errore secondario e il testo dell’errore sono specificati dal server BEES all’interno del file della risposta JSON `error` e `errorText` proprietà. Questo tipo di risposta non deve essere considerato un errore, ma piuttosto una risposta di rifiuto regolare da parte del server BEES. |
