---
title: SSO di Amazon FireOS utilizzando il manuale API senza client
description: SSO di Amazon FireOS utilizzando il manuale API senza client
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# SSO di Amazon FireOS utilizzando il manuale API senza client {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Introduzione {#Introduction}

Questo documento fornisce istruzioni per implementare la versione SSO di Amazon del flusso di autenticazione di Adobe Primetime utilizzando l’API senza client. La prima parte di questo documento si concentra sulla specificità della versione Amazon dell’architettura, per i molti partner che già conoscono e hanno esperienza con la sua implementazione.

La seconda parte del documento illustra i passaggi principali per implementare l’API senza client di Adobe Primetime Authentication.

Per una panoramica tecnica del funzionamento della soluzione Clientless, vedi [Panoramica API REST](/help/authentication/rest-api-overview.md). L’Adobe è il contatto preferito per il supporto relativo all’architettura generale e alle prime implementazioni.

## SSO senza client di Amazon {#AMZ-Clientless-SSO}

### Architettura di alto livello {#High-Level-Arch}

L’implementazione SSO senza client di Amazon è semplice e per lo più identica alle normali API senza client di autenticazione di Adobe Primetime.

Dovrai utilizzare l’SDK di Amazon per recuperare un payload personalizzato e utilizzarlo quando richiami le API Adobe clientless.

Se il payload viene riconosciuto e corrisponde a una sessione autenticata, le API senza client torneranno immediatamente con il token della sessione.

### Come creare l’applicazione per utilizzare l’SDK di Amazon {#Build-entries}

* Scarica e copia la versione più recente [SDK stub di Amazon](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) in una cartella /SSOEnabler parallela alla directory dell’app
* Aggiorna i file manifest/gradle per utilizzare la libreria:

  **Aggiungi la seguente riga al file Manifest:**

  ```Java
  <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
  ```

  **Voci file gradle:**

  In archivi:

  ```java
  flatDir {
       dirs '../SSOEnabler'
  }
  ```

  In dipendenze, aggiungi:

  ```Java
  provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
  ```


* Gestione dell’assenza dell’app ausiliaria Amazon:

  Anche se è improbabile che, nel caso in cui il dispositivo ausiliario non sia presente sul dispositivo Amazon in esecuzione nell’applicazione, venga rilevata un’eccezione ClassNotFoundException in fase di esecuzione sulla classe seguente: `com.amazon.ottssotokenlib.SSOEnabler`.

  In questo caso, tutto ciò che devi fare è saltare il passaggio di payload e tornare al normale flusso PrimeTime. SSO non verrà abilitato, ma il flusso di autenticazione regolare si verificherà normalmente.

</br>

### Ottenere il payload SSO di Amazon con l’SDK di Amazon {#UseAmazonSSO}

Durante l&#39;inizializzazione dell&#39;applicazione, ottenere un&#39;istanza di SSOEnabler. In base all’architettura dell’applicazione, è necessario scegliere tra un’implementazione sincrona o asincrona.

Se per qualsiasi motivo le chiamate API non restituiscono un payload, utilizza il flusso non SSO regolare e contatta il tuo Amazon e i partner Adobe per effettuare un’indagine.

**API asincrona**

* Ottieni istanza di SSO Enabler:

  ```Java
  ssoEnabler = SSOEnabler.getInstance(context);
  SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
  ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
  ```


* Impostare il callback

  ```java
  public static abstract class SSOEnablerCallback
  {
          public abstract void getSSOTokenSuccess(Bundle result);
          public abstract void getSSOTokenFailure(Bundle result);
  }
  ```

   * Il bundle di risposta di successo conterrà:
      * Token SSO come stringa con chiave &quot;SSOToken&quot;
   * Il bundle di risposta degli errori conterrà:
      * codice di errore come int con chiave &quot;ErrorCode&quot;
      * descrizione dell’errore come stringa con chiave &quot;ErrorDescription&quot;


* Ottieni token SSO

  ```JAVA
  Bundle getSSOTokenAsync(Void);
  ```

* Questa API fornirà la risposta tramite callback impostato durante l’inizializzazione.

  **Es**. chiama utilizzando l’istanza singleton creata durante l’inizializzazione:

  ```JAVA
  ssoEnabler.getSSOTokenAsync().
  ```


**API sincrone**

* Ottieni l’istanza di SSO Enabler e imposta il callback

  ```JAVA
  ssoEnabler = SSOEnabler.getInstance(context);</span>
  ```

* Ottieni token SSO

  ```JAVA
  Bundle getSSOTokenSync(Void);
  ```

   * Questa API blocca il thread chiamante e risponde con il bundle dei risultati. Poiché si tratta di una chiamata sincrona, non utilizzarla nel thread principale.

  ```JAVA
  void setSSOTokenTimeout(long);
  ```

   * Valore in millisecondi. se questa opzione è impostata, sovrascrivi il valore di timeout predefinito di 1 minuto per l’API di sincronizzazione.


### Aggiornamento API di Adobe Primetime Clientless per utilizzare la registrazione client dinamica {#clientlessdcr}

Se si tratta della prima implementazione, consulta la sezione **Panoramica tecnica senza client** e contatta l’Adobe nel caso tu abbia bisogno di supporto.

L’API Adobe Clientless richiede che le applicazioni utilizzino la registrazione client dinamica per effettuare chiamate ai server Adobe.

* Per utilizzare Registrazione client dinamica nell&#39;applicazione, seguire le istruzioni riportate in [Dynamic Client Registration Management per registrare l&#39;applicazione](/help/authentication/dynamic-client-registration-management.md).

* Per implementare l’API di registrazione client dinamica per eseguire le richieste di autenticazione e autorizzazione ai server Adobe Primetime, segui le istruzioni in [API di registrazione client dinamici](/help/authentication/dynamic-client-registration-api.md) .

### Aggiornamento API Adobe Primetime Clientless per l’utilizzo di Amazon SSO {#clientlesssso}

Il payload SSO di Amazon ottenuto dall’SDK di Amazon deve essere presente nelle richieste effettuate agli endpoint di autenticazione di Adobe Primetime:

```
      /adobe-services/*
      /reggie/*
      /api/*
```


Tutti gli endpoint di autenticazione Primetime supportano i seguenti metodi per ricevere l’identificatore con ambito dispositivo o con ambito piattaforma (presente nel payload SSO SSO di Amazon):

* Come intestazione : &quot;Adobe-Subject-Token&quot;
* Come parametro di query : &quot;ast&quot;
* Come parametro post : &quot;ast&quot;


>[!NOTE]
>
>Se l’identificatore con ambito dispositivo o con ambito piattaforma viene inviato come parametro query/post, deve essere incluso durante la generazione della firma della richiesta.

>[!NOTE]
>
>Utilizzando il parametro di query &quot;ast&quot;, l’intero URL potrebbe diventare molto lungo e rifiutato. Nella chiamata /authenticate, questo parametro può essere ignorato poiché è stato fornito nella chiamata /regcode

**Esempi:**

**Invio come intestazione personalizzata**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**Invio come parametro di query**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**Invio come parametro post**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>Se l’SSO di Amazon non è presente o non è valido, l’autenticazione di Adobe Primetime ignorerà l’attributo e le chiamate verranno eseguite come se l’SSO non fosse presente.
