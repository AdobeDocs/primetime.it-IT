---
title: Identificazione delle risorse protette
description: Identificazione delle risorse protette
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Identificazione delle risorse protette {#identifying-protected-resources}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

Ogni richiesta di autorizzazione (o richiesta di controllo dell&#39;autorizzazione) deve contenere un identificatore univoco per la risorsa protetta per la quale l&#39;utente richiede l&#39;accesso. Una risorsa protetta può essere qualsiasi livello di contenuto autorizzato, come concordato tra un MVPD e i programmatori partecipanti. Le potenziali risorse protette devono inserirsi in questa struttura ad albero con granularità sempre più specifica:

- Rete
   - Canale
      - Mostra
         - Episodio
            - Risorsa\
                

</br>

## Formato RSS Media {#media_rss}

Le risorse possono essere identificate da una stringa semplice (un identificatore univoco per un canale), oppure possono essere rappresentate in formato Media RSS (MRSS), come concordato tra l&#39;Adobe (o un partner autorizzato per l&#39;autenticazione Adobe Primetime) e gli MVPD e i programmatori partecipanti. La stringa RSS utilizzata come identificatore di risorse può includere informazioni aggiuntive, ad esempio valutazioni e metadati di controllo genitori.\
 

Se si utilizza un identificatore di risorsa semplice, ad esempio &quot;TNT&quot;, si presume che rappresenti un canale e viene convertito in questo identificatore di risorse RSS:

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

Un identificatore più complesso può includere, ad esempio, informazioni aggiuntive di valutazione. È possibile passare l&#39;intera stringa RSS alle funzioni di Access Enabler che richiedono un ID risorsa, ad esempio [`getAuthorization()`](/help/authentication/rest-api-reference.md):

```rss
    var resource = 
        '<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/"> 
             <channel>
                 <title>TNT</title>
                 <media:rating scheme="urn:mpaa">pg</media:rating>
             </channel>
         </rss>'; 
    getAuthorization(resource);
```

Gli identificatori di risorsa sono opachi all’autenticazione Adobe Primetime; vengono semplicemente trasmesse al MVPD. Se l’MVPD non riconosce o non può analizzare l’identificatore di risorse, restituisce un errore all’autenticazione Adobe Primetime, che riporta l’errore al `tokenRequestFailed()` callback.

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->