---
title: Codici di errore BEES
description: Codici di errore BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Codici di errore BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Se si verifica un errore durante un controllo BEES, viene restituito al client un `DRMErrorEvent`. Puoi analizzare le proprietà di questo evento per trovare dettagli sulla natura dell&#39;errore. Di seguito è riportato un sottoinsieme di possibili codici di errore.

| Errore | Descrizione |
|---|---|
| `3304:305` | Errore di autorizzazione generico da DRM di Primetime Cloud che tenta di gestire una richiesta di autenticazione/autorizzazione. In genere non associata a un problema API. Se questo errore viene rilevato in modo coerente, è necessario inviare un ticket di problemi al team DRM di Primetime Cloud insieme alle informazioni di diagnostica. |
| `3329:0` | Errore specifico dell&#39;applicazione (dall&#39;autore BEES). Se non è stato restituito alcun codice di errore secondario, nel testo di errore vengono visualizzati i dettagli del problema. Ad esempio, si è verificato un problema durante l’analisi della risposta, oppure il server BEES non era raggiungibile. |
| `3329:<HTTP error code>` | Una risposta HTTP diversa da 200 è stata emessa dal server BEES. Il codice di errore HTTP viene restituito al client nel campo del codice del sottoerrore. Questo potrebbe indicare un problema di configurazione o un&#39;interruzione del server BEES. |
| `3329:<x>` | Server BEES HA CONSENTITO la richiesta di licenza. Il codice di errore secondario e il testo di errore sono specificati dal server BEES all’interno delle proprietà `error` e `errorText` della risposta JSON. Questo tipo di risposta non dovrebbe essere considerato un errore, ma piuttosto una risposta di rifiuto regolare dal server BEES. |