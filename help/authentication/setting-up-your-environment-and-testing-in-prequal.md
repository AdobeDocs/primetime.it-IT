---
title: Configurazione dell’ambiente e test in Pre-Qual
description: Configurazione dell’ambiente e test in Pre-Qual
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Configurazione dell’ambiente e test in Pre-Qual{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

Questa nota tecnica ha lo scopo di aiutare i nostri partner a configurare il proprio ambiente e a iniziare a testare una nuova build implementata nell’ambiente di prequalifica Adobe.

Poiché esistono due tipi di build: ***produzione*** e ***staging***, in questo documento ci concentreremo sulla configurazione di produzione con la menzione che tutti i passaggi sono gli stessi per la gestione temporanea, solo gli URL sono diversi.

I passaggi 1 e 2 stanno configurando l’ambiente di test su una delle macchine di test, il passaggio 3 è una verifica del flusso di base e i passaggi 4 e 5 presentano alcune linee guida per i test.

>[!IMPORTANT]
>
> È molto importante eseguire i passaggi 1 e 2 ogni volta che desideri modificare l’ambiente di test (passando dalla gestione temporanea al profilo di produzione o viceversa)
 

## PASSAGGIO 1: Risoluzione del passaggio del dominio a un IP {#resolving-pass-domain-to-an-ip}

* Per trovare un IP del load balancer che possa essere utilizzato per lo spoofing, eseguire il comando seguente:

* **Su Windows**

   ```cmd
   C:\>nslookup sp-prequal.auth.adobe.com
   ...
   Addresses:  52.13.71.11
               54.184.208.150
   ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **Su Linux/Mac**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>Domini esclusi dalla risposta in quanto non rilevanti e possono differire da utente a utente.

>[!IMPORTANT]
>
> Questi indirizzi IP potrebbero cambiare in futuro e potrebbero non essere gli stessi per gli utenti in diverse aree geografiche.


## PASSAGGIO 2:  Spoofing dell’ambiente di pre-qualificazione per la produzione {#spoofing-the-prequalification-environment}

* Modifica il *c:\\windows\\System32\\drivers\\etc\\hosts* file (in Windows) o */etc/hosts* (su Macintosh/Linux/Android) e aggiungere quanto segue:

* Profilo di produzione spoof
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Spoofing su Android:** Per falsificare su Android, devi utilizzare un emulatore Android.

* Una volta attivato lo spoofing, puoi semplicemente utilizzare gli URL regolari per i profili di produzione e staging: `http://sp.auth-staging.adobe.com` e `http://entitlement.auth-staging.adobe.com` e si raggiungerà il *ambiente/produzione di pre-qualificazione* della nuova build*.


## PASSAGGIO 3:  Verifica che tu stia puntando all’ambiente giusto {#Verify-you-are-pointing-to-the-right-environment}

**Questo è un passaggio semplice:**

* carica [diritto preuguale ambiente](https://entitlement-prequal.auth.adobe.com/environment.html) e [adesione](https://entitlement.auth.adobe.com/environment.html). Devono restituire la stessa risposta.


## PASSAGGIO 4:  Eseguire un semplice flusso di autenticazione/autorizzazione utilizzando il sito Web del programmatore {#peform-a-simple-auth-flow}

* Questo passaggio richiede l’indirizzo del sito web del programmatore e alcune credenziali MVPD valide (un utente autenticato e autorizzato).

## PASSAGGIO 5:  Eseguire il test dello scenario utilizzando i siti Web del programmatore {#perform-scenario-testing-using-programmer-website}

* Dopo aver completato la configurazione dell’ambiente e aver verificato il funzionamento del flusso di autenticazione-autorizzazione di base, puoi procedere con il test di scenari più complessi.


## PASSAGGIO 6:  Eseguire test utilizzando il sito di test API {#perform-testing-using-api-testing-site}

* Per una verifica più approfondita dell’autenticazione di Adobe Primetime, ti consigliamo di utilizzare [Sito di test API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Per ulteriori dettagli sul sito di test API, consulta [Verificare i flussi di autenticazione e autorizzazione utilizzando il sito di test API di Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
