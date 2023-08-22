---
title: Configurazione dell’ambiente e test in Pre-Qual
description: Configurazione dell’ambiente e test in Pre-Qual
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Configurazione dell&#39;ambiente e test in pre-qual{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>I contenuto in questa pagina sono forniti solo a scopo informativo. L&#39;utilizzo di questa API richiede una licenza corrente da Adobe Systems. Non è consentito alcun utilizzo non autorizzato.

Lo scopo di questa nota tecnica è quello di aiutare i nostri partner a configurare il loro ambiente e iniziare a testare una nuova versione distribuita nell&#39;ambiente di Adobe Systems pre-qualifica.

Poiché esistono due versione gusti: ***produzione*** e ***staging*** , in questo documento concentrarsi nella configurazione di produzione con la menzione che tutti i passaggi sono uguali per la gestione temporanea, solo gli URL sono diversi.

I passaggi 1 e 2 stanno impostando l&#39;ambiente di test su uno dei computer di prova, il passaggio 3 è una verifica del flusso di base e i passaggi 4 e 5 presentano alcune linee guida di test.

>[!IMPORTANT]
>
> È molto importante eseguire i passaggi 1 e 2 ogni volta che si desidera modificare l&#39;ambiente di testing (passaggio dalla gestione temporanea al profilo di produzione o al contrario)


## PASSAGGIO 1: Risoluzione del passaggio del dominio a un IP {#resolving-pass-domain-to-an-ip}

* Per trovare un IP del load balancer che possa essere utilizzato per lo spoofing, eseguire il comando seguente:

* **Su Windows**

  ```cmd
  C:\>nslookup sp-prequal.auth.adobe.com
  ...
  Addresses:  52.13.71.11
              54.184.208.150
  ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **Su Linux/Mac**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>I domini esclusi dalla risposta non sono rilevanti e potrebbero differire da utente a utente.

>[!IMPORTANT]
>
> Questi indirizzi IP possono cambiare in futuro e potrebbero non essere uguali per gli utenti di diverse aree geografiche.


## PASSAGGIO 2.  Spoofing dell&#39;ambiente di pre-qualifica per la produzione {#spoofing-the-prequalification-environment}

* Modifica il *file C:\\windows\\system32\\drivers\\etc\\hosts* (in Windows) o */etc/hosts* (su Macintosh/Linux/Android) e Aggiungi quanto segue:

* Profilo di produzione spoof
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Spoofing su Android:** Per falsificare su Android, devi utilizzare un emulatore Android.

* Una volta attivato lo spoofing, puoi semplicemente utilizzare gli URL regolari per i profili di produzione e staging: `http://sp.auth-staging.adobe.com` e `http://entitlement.auth-staging.adobe.com` e si raggiungerà il *ambiente/produzione di pre-qualificazione* della nuova build*.


## PASSAGGIO 3:  Verifica che tu stia puntando all’ambiente giusto {#Verify-you-are-pointing-to-the-right-environment}

**Questo è un passaggio semplice:**

* carica [ l&#39;ambiente ](https://entitlement-prequal.auth.adobe.com/environment.html) e [ il diritto ](https://entitlement.auth.adobe.com/environment.html) di PreQual titolarità. Devono restituire la stessa risposta.


## PASSAGGIO 4.  Esegui un semplice flusso di autenticazione/autorizzazione utilizzando il sito Web del programmatore {#peform-a-simple-auth-flow}

* Questo passaggio richiede l&#39;indirizzo del sito Web del programmatore e alcune credenziali MVPD valide (una utente che è autenticata e autorizzata).

## PASSAGGIO 5.  Esecuzione di test di scenario con i siti Web del programmatore {#perform-scenario-testing-using-programmer-website}

* Dopo aver completato la configurazione dell&#39;ambiente e aver fatto sì che il flusso di autorizzazione di base sia funzionante, puoi procedere con la verifica di scenari più complessi.


## PASSAGGIO 6:  Eseguire test utilizzando il sito di test API {#perform-testing-using-api-testing-site}

* Per una verifica più approfondita dell’autenticazione di Adobe Primetime, ti consigliamo di utilizzare [Sito di test API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Per ulteriori dettagli sul sito di test API, consulta [Verificare i flussi di autenticazione e autorizzazione utilizzando il sito di test API di Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
