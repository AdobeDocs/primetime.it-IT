---
title: Appendice B "Suggerimenti per il debug"
description: Appendice B "Suggerimenti per il debug"
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Appendice B: Suggerimenti per il debug {#appendix-b-debugging-tips}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Cancellazione dei dati temporanei {#clearing-temporary-data}

L’autenticazione Adobe Primetime memorizza dati temporanei quali la cache del browser, la cache degli LSO e i cookie. La cancellazione dei dati temporanei è importante, per assicurarti di ottenere una lavagna pulita durante il test.

- [Cancellazione della cache del browser e dei cookie](#clearing-the-browser-cache-and-cookies)
- [Cancellazione della cache degli LSO](#clearing-lsos-cache)\
    

## Cancellazione della cache del browser e dei cookie {#clearing-the-browser-cache-and-cookies}

È affidabile per il browser, ma in Firefox: &quot;Strumenti&quot; -\> &quot;Cancella cronologia recente..&quot; -\> Su &quot;Intervallo di tempo da cancellare:&quot; selezionare &quot;Tutto&quot;; e su &quot;Dettagli&quot;: controlla &quot;Cookies&quot; e &quot;Cache&quot; -\> Fai clic su &quot;Cancella ora&quot;.\
 

## Cancellazione della cache degli LSO {#clearing-lsos-cache}

Accedere al [Guida del Flash Player](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

Seleziona la ```entitlement.\*``` (a seconda di ciò che viene testato) e fare clic su &quot;Elimina sito Web&quot;.\
 

## Strumenti di debug {#tools}

Gli ingegneri di autenticazione di Adobe Primetime utilizzano i seguenti strumenti di debug:

- Firebug - <http://www.getfirebug.com/>
- Flashbug (funziona con la versione di debug del flash player) <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- Intestazioni http live - <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- Charles - <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->