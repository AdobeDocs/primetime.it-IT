---
seo-title: Codici di errore BEES
title: Codici di errore BEES
uuid: 7b2d0dd1-9a43-47e3-b932-a4eaf784ae7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Codici di errore BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Se si verifica un errore durante un controllo BEES, `DRMErrorEvent` verrà restituito un errore al client. È possibile analizzare le proprietà dell&#39;evento per ottenere informazioni dettagliate sulla natura dell&#39;errore. Di seguito è riportato un sottoinsieme di possibili codici di errore.

| Errore | Descrizione |
|---|---|
| `3304:305` | Errore di autorizzazione generica da DRM di Primetime Cloud che tenta di gestire una richiesta di autenticazione/autorizzazione. Generalmente non associato a un problema BEES. Se l&#39;errore viene rilevato in modo coerente, è necessario inviare un ticket di problemi al team DRM di Primetime Cloud insieme alle informazioni di diagnostica. |
| `3329:0` | Errore specifico dell&#39;applicazione (dall&#39;autore BEES). Se non viene restituito alcun codice di errore secondario, nel testo di errore vengono visualizzati i dettagli del problema. Ad esempio, si è verificato un problema durante l&#39;analisi della risposta, oppure il server BEES non era raggiungibile. |
| `3329:<HTTP error code>` | Una risposta HTTP diversa da 200 è stata emessa dal server BEES. Il codice di errore HTTP viene restituito al client nel campo del codice di errore secondario. Ciò potrebbe indicare un problema di configurazione o un&#39;interruzione del server BEES. |
| `3329:<x>` | Server BEES HA CONSENTITO la richiesta di licenza. Il codice di errore secondario e il testo di errore sono specificati dal server BEES all&#39;interno delle proprietà `error` e `errorText` della risposta JSON. Questo tipo di risposta non dovrebbe essere considerato un errore, ma piuttosto una risposta di rifiuto regolare da parte del server BEES. |