---
title: Aggiornamenti dei cookie - Flag SameSite e Secure
description: Aggiornamenti dei cookie - Flag SameSite e Secure
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---



# Aggiornamenti dei cookie - Flag SameSite e Secure {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>


## Aggiornamenti {#Updates}

Questa sezione evidenzia le modifiche introdotte dal browser Chrome e dall’autenticazione Adobe Primetime per la gestione dei cookie di terze parti.

 

### Aggiornamenti di Chrome 80 {#Chrome}

A partire da Chrome versione 80 (eccetto versione 82), cookie che non specificano un *SameSite* l&#39;attributo sarà trattato come se fossero *SameSite=Lax*. Pertanto, i cookie che devono essere consegnati in un contesto intersito devono specificare esplicitamente la variabile *SameSite=None* e deve inoltre essere contrassegnato con *Secure* attributo e consegnato *HTTPS*. Maggiori dettagli su questi aggiornamenti possono essere letti dalla pagina ufficiale del cromo: <https://www.chromium.org/updates/same-site> e anche da <https://web.dev/samesite-cookies-explained/>.


### Aggiornamenti dell’autenticazione di Adobe Primetime {#Pass-Updates}

Il servizio di autenticazione di Adobe Primetime si avvale attualmente di un paio di cookie considerati cookie di terze parti dal punto di vista del browser, incluso Chrome, per funzionare in combinazione con alcune piattaforme e versioni degli SDK di autenticazione di Adobe Primetime. Pertanto, per rispettare le prossime modifiche e continuare a distribuire questi cookie in un contesto intersito da questi SDK meno recenti, il servizio Adobe Primetime Authentication implementa le modifiche richieste nel *adobe-pass-2.55.1* versione.

Queste modifiche dal *adobe-pass-2.55.1* alla versione è necessario aggiungere *Secure* e *SameSite=None* attributi per tutti i cookie passati a tutti gli SDK di autenticazione Adobe Primetime quando si utilizzano browser Chrome a partire dalla versione 80 e successive (eccetto la versione 82).

La sezione successiva presenta alcuni potenziali problemi per un elenco di piattaforme e versioni degli SDK per l’autenticazione di Adobe Primetime nel caso in cui un utente utilizzi il browser Chrome 80 e versioni successive (eccetto la versione 82).

## Risoluzione dei problemi {#Troubleshooting}

Durante la navigazione in questa sezione ricorda che tutti i cookie del servizio di autenticazione Adobe Primetime devono avere *Secure* attributo impostato in *adobe-pass-2.55.1* per tutti i browser, mentre *SameSite=None* L’attributo deve essere impostato solo per i browser Chrome versione 80 e successive (eccetto versione 82).


### Risoluzione dei problemi generali {#General}

1. Importante notare che alcuni agenti utente sono notoriamente incompatibili con il *SameSite=None* attributo.

   - Versioni di Chrome da Chrome 51 a Chrome 66 (incluso su entrambe le estremità). Queste versioni di Chrome rifiuteranno un cookie con *SameSite=None*. Questo interessa anche le versioni precedenti dei browser derivati da Chromium e Android WebView. Questo comportamento era corretto in base alla versione della specifica del cookie in quel momento, ma con l’aggiunta del nuovo valore &quot;None&quot; alla specifica, questo comportamento è stato aggiornato in Chrome 67 e versioni successive. (Prima di Chrome 51, l’attributo SameSite veniva ignorato completamente e tutti i cookie venivano trattati come se fossero *SameSite=None*.)
   - Versioni di UC Browser su Android prima della versione 12.13.2. Le versioni precedenti rifiuteranno un cookie con *SameSite=None*. Questo comportamento era corretto in base alla versione della specifica del cookie in quel momento, ma con l&#39;aggiunta del nuovo valore &quot;None&quot; alla specifica, questo comportamento è stato aggiornato nelle versioni più recenti di UC Browser.
   - Versioni di Safari e browser incorporati in MacOS 10.14 e tutti i browser in iOS 12. Queste versioni tratteranno erroneamente i cookie contrassegnati con *SameSite=None* come se fossero marcati *SameSite=Strict*. Questo bug è stato corretto nelle versioni più recenti di iOS e MacOS.


1. Importante notare che i cookie hanno *Secure* l&#39;attributo deve essere inviato *HTTPS* in caso contrario, il cookie non raggiunge il servizio di autenticazione di Adobe Primetime.

   - SDK JavaScript di AccessEnabler:
      - Obbligatorio che la comunicazione con *sp.auth.adobe.com* utilizza *HTTPS* per le versioni *2,35* e *3.5.0*, prima di introdurre la Registrazione client dinamica.
   - AccessEnabler iOS/tvOS SDK:
      - Obbligatorio che la comunicazione con *sp.auth.adobe.com* utilizza *HTTPS* per le versioni precedenti a *3,0*, prima di introdurre la Registrazione client dinamica.
   - SDK per Android di AccessEnabler:
      - Obbligatorio che la comunicazione con *sp.auth.adobe.com* utilizza *HTTPS* per le versioni precedenti a *3,0*, prima di introdurre la Registrazione client dinamica.
   - AccessEnabler FireOS SDK:
      - Obbligatorio che la comunicazione con *sp.auth.adobe.com* utilizza *HTTPS* per versione *2.0.4*.

</br>

### Risoluzione dei problemi di AccessEnabler JavaScript SDK versione 2.35 {#235-Troubleshooting}

Il flusso di autenticazione dell&#39;utente potrebbe essere interessato in Chrome 80 e versioni successive (eccetto versione 82). Per assicurarsi che l&#39;utente non abbia problemi di autenticazione a causa degli aggiornamenti di cui sopra è possibile:

- Controlla che la *JSESSIONID* il cookie è impostato nel browser e ha *SameSite=None* e *Secure* attributi impostati. 
- Controlla che la *JSESSIONID* cookie dal *https://sp.auth.adobe.com/authenticate/saml* la richiesta di rete corrisponde alla *JSESSIONID* cookie dal *https://sp.auth.adobe.com/session* richiesta di rete.


### Risoluzione dei problemi di AccessEnabler JavaScript SDK versione 3.5.0 {#350-Troubleshooting}

Il flusso di autenticazione dell&#39;utente potrebbe essere interessato in Chrome 80 e versioni successive (eccetto versione 82). Per assicurarsi che l&#39;utente non abbia problemi di autenticazione a causa degli aggiornamenti di cui sopra è possibile:

- Controlla che la *JSESSIONID* il cookie è impostato nel browser e ha *SameSite=None* e *Secure* attributi impostati. 
- Controlla che la *JSESSIONID* cookie dal *https://sp.auth.adobe.com/authenticate/saml* la richiesta di rete corrisponde alla *JSESSIONID* cookie dal *https://sp.auth.adobe.com/session* richiesta di rete.
- Controlla che la *pass\_sfp* il cookie è impostato nel browser e ha *SameSite=None* e *Secure* attributi impostati.
- Controlla che la *pass\_sfp* cookie impostato in *https://sp.auth.adobe.com/session* richiesta di rete.


Il flusso di autorizzazione dell&#39;utente potrebbe essere influenzato in Chrome 80 e versioni successive (eccetto versione 82). Al fine di assicurarsi che l&#39;utente non abbia problemi a guardare una risorsa protetta, dopo essere stato autenticato con successo, a causa degli aggiornamenti di cui sopra si può:

- Controlla che la *pass\_sfp* il cookie è impostato nel browser e ha *SameSite=None* e *Secure* attributi impostati.
- Controlla che la *pass\_sfp* cookie impostato in *https://sp.auth.adobe.com/adobe-services/authorize* richiesta di rete.
- Controlla che la *pass\_sfp* cookie impostato in *https://sp.auth.adobe.com/adobe-services/shortAuthorize* richiesta di rete.
