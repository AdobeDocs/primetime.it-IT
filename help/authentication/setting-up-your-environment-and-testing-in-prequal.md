---
title: Impostazione dell'ambiente e test in Pre-Qual
description: Impostazione dell'ambiente e test in Pre-Qual
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Impostazione dell&#39;ambiente e test in Pre-Qual{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

Lo scopo di questa nota tecnica è aiutare i nostri partner a configurare il loro ambiente e iniziare a testare una nuova build implementata nell’ambiente di pre-qualificazione Adobe.

Dal momento che ci sono due sapori da costruzione: ***produzione*** e ***staging*** In questo documento ci concentreremo sulla configurazione di produzione con la menzione che tutti i passaggi sono gli stessi per la gestione temporanea, solo gli URL sono diversi.

I passaggi 1 e 2 impostano l&#39;ambiente di prova su una delle macchine di prova, il passaggio 3 è una verifica del flusso di base e i passaggi 4 e 5 presentano alcune linee guida di prova.

>[!IMPORTANT]
>
> È molto importante eseguire i passaggi 1 e 2 ogni volta che si desidera modificare l’ambiente di test (passaggio dalla fase di staging al profilo di produzione o viceversa)
 

## PASSAGGIO 1. Risoluzione del dominio Pass su un IP {#resolving-pass-domain-to-an-ip}

* Per trovare un IP del load balancer che può essere utilizzato per lo spoofing, esegui il seguente comando:

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
>Domini esclusi dalla risposta in quanto non sono rilevanti e potrebbero differire da utente a utente.

>[!IMPORTANT]
>
> Questi indirizzi IP potrebbero cambiare in futuro e potrebbero non essere gli stessi per gli utenti di diverse aree geografiche.


## PASSAGGIO 2.  Come spoofing dell’ambiente di pre-qualificazione per la produzione {#spoofing-the-prequalification-environment}

* Modifica le *c:\\windows\\System32\\drivers\\etc\\hosts* file (in Windows) o */etc/hosts* file (su Macintosh/Linux/Android) e aggiungi quanto segue:

* Profilo di produzione spogliato
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Spoofing su Android:** Per spoof su Android, è necessario utilizzare un emulatore Android.

* Una volta implementato lo spoofing, puoi semplicemente utilizzare gli URL regolari per i profili di produzione e di staging: (ossia `http://sp.auth-staging.adobe.com` e `http://entitlement.auth-staging.adobe.com` e colpirai il *ambiente/produzione pre-qualificazione* della nuova build*.


## PASSAGGIO 3.  Verifica di puntare all’ambiente corretto {#Verify-you-are-pointing-to-the-right-environment}

**Questo è un passo facile:**

* carico [ambiente prepari di adesione](https://entitlement-prequal.auth.adobe.com/environment.html) e [diritto](https://entitlement.auth.adobe.com/environment.html). Dovrebbero dare la stessa risposta.


## PASSAGGIO 4.  Eseguire un semplice flusso di autenticazione/autorizzazione utilizzando il sito web del programmatore {#peform-a-simple-auth-flow}

* Questo passaggio richiede l&#39;indirizzo del sito web del programmatore e alcune credenziali MVPD valide (un utente autenticato e autorizzato).

## PASSAGGIO 5.  Eseguire test di scenario utilizzando i siti web del programmatore {#perform-scenario-testing-using-programmer-website}

* Dopo aver completato la configurazione dell&#39;ambiente e aver verificato il funzionamento del flusso di autorizzazione dell&#39;autenticazione di base, puoi procedere con il test di scenari più complessi.


## PASSAGGIO 6.  Esegui test utilizzando il sito di test API {#perform-testing-using-api-testing-site}

* Per approfondire la verifica dell’autenticazione di Adobe Primetime, ti consigliamo di utilizzare il [Sito di test API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Per ulteriori dettagli sul sito di test API, visita [Come testare i flussi di autenticazione e autorizzazione utilizzando il sito di test API di Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

