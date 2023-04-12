---
title: Amazon FireOS SSO tramite il cookie API Clientless
description: Amazon FireOS SSO tramite il cookie API Clientless
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---


# Amazon FireOS SSO tramite il cookie API Clientless {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Introduzione {#Introduction}

Questo documento fornisce istruzioni per implementare la versione SSO di Amazon del flusso di autenticazione di Adobe Primetime utilizzando l&#39;API senza client. La prima parte di questo documento si concentra sulla specificità della versione Amazon dell’architettura, per i molti partner che hanno già familiarità ed esperienza con la sua implementazione.

La seconda parte del documento descrive i passaggi principali per implementare l’API senza client di Adobe Primetime Authentication.

Per un&#39;ampia panoramica tecnica del funzionamento della soluzione Clientless, vedi [Panoramica API REST](/help/authentication/rest-api-overview.md). Adobe è il contatto preferito per il supporto sull’architettura complessiva e le prime implementazioni.

## SSO senza client Amazon {#AMZ-Clientless-SSO}

### Architettura di alto livello {#High-Level-Arch}

L&#39;implementazione SSO senza client di Amazon è semplice e per lo più identica alle normali API senza client di Adobe Primetime Authentication.

Per recuperare un payload personalizzato e utilizzarlo per chiamare le API senza client di Adobe, devi utilizzare l’SDK di Amazon.

Se il payload viene riconosciuto e corrisponde a una sessione autenticata, le API senza client torneranno immediatamente con il token della sessione.

### Come creare l&#39;applicazione per utilizzare l&#39;SDK di Amazon {#Build-entries}

* Scarica e copia l’ultima [Amazon Stub SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) in una cartella /SSOEnabler parallela alla directory dell&#39;app
* Aggiorna i file manifest/gradle per utilizzare la libreria :

   **Aggiungi la seguente riga al file Manifest:**

   ```Java
   <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
   ```

   **Voci dei file di livello:**

   Sotto archivi:

   ```java
   flatDir {
        dirs '../SSOEnabler'
   }
   ```

   In dipendenze, aggiungi:

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* Gestione dell’assenza della companion app Amazon:

   Anche se non è probabile, se la compagna non è presente sul dispositivo Amazon in esecuzione nella tua applicazione, dovresti incontrare una ClassNotFoundException in fase di runtime sulla seguente classe: `com.amazon.ottssotokenlib.SSOEnabler`.

   In questo caso, tutto quello che devi fare è saltare il passaggio del payload e cadere sul normale flusso PrimeTime. L&#39;SSO non verrà attivato ma il flusso di autenticazione regolare avverrà normalmente.

</br>

### Come ottenere il payload Amazon SSO con l’SDK di Amazon {#UseAmazonSSO}

Durante l&#39;inizializzazione dell&#39;applicazione, ottenere un&#39;istanza di SSOEnabler. In base all’architettura dell’applicazione, dovresti decidere se implementare in modo sincrono o asincrono.

Se per qualsiasi motivo, le chiamate API non restituiscono un payload, utilizza il flusso non SSO regolare e contatta i tuoi partner Amazon e Adobe per indagare.

**API asincrona**

* Ottieni l&#39;istanza SSO Enabler:

   ```Java
   ssoEnabler = SSOEnabler.getInstance(context);
   SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
   ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
   ```


* Imposta il callback 

   ```java
   public static abstract class SSOEnablerCallback
   {
           public abstract void getSSOTokenSuccess(Bundle result);
           public abstract void getSSOTokenFailure(Bundle result);
   }
   ```

   * Il bundle di risposta di successo conterrà:
      * Token SSO come stringa con la chiave &quot;SSOToken&quot;
   * Il bundle di risposta di errore conterrà:
      * codice di errore come int con la chiave &quot;ErrorCode&quot;
      * descrizione dell’errore come stringa con la chiave &quot;ErrorDescription&quot;


* Ottieni token SSO

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* Questa API fornirà la risposta tramite callback impostato durante l’init.

   **Ex**. chiama utilizzando l’istanza singleton creata durante init:

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**API sincrone**

* Ottieni l&#39;istanza SSO Enabler e imposta il callback

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* Ottieni token SSO

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * Questa API bloccherà il thread del chiamante e risponderà con il pacchetto di risultati. Poiché si tratta di una chiamata sincrona, assicurati di non utilizzarla nel thread principale.

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * Valore in millisecondi. se impostato, ignora il valore di timeout predefinito di 1 minuto per l’API di sincronizzazione.



### Aggiornamento dell’API Adobe Primetime Clientless per utilizzare la registrazione client dinamica {#clientlessdcr}

Se questa è la tua prima implementazione, consulta **Panoramica tecnica senza client** e contatta l’Adobe nel caso in cui ti occorra supporto.

Adobe Clientless API richiede che le applicazioni utilizzino la Registrazione client dinamica per effettuare chiamate ai server Adobe.

* Per utilizzare la Registrazione client dinamica nella tua applicazione, segui le istruzioni in [ Dynamic Client Registration Management per registrare l&#39;applicazione](/help/authentication/dynamic-client-registration-management.md).

* Per implementare l’API di registrazione client dinamica per eseguire richieste di autenticazione e autorizzazione ai server Adobe Primetime, segui le istruzioni in [API di registrazione client dinamica](/help/authentication/dynamic-client-registration-api.md) .

### Aggiornamento dell’API Adobe Primetime Clientless per utilizzare Amazon SSO {#clientlesssso}

Il payload SSO Amazon ottenuto dall’SDK di Amazon deve essere presente nelle richieste effettuate agli endpoint di autenticazione Adobe Primetime :

```
      /adobe-services/*
      /reggie/*
      /api/*
```


Tutti gli endpoint di autenticazione di Primetime supportano i seguenti metodi per ricevere l&#39;identificatore con ambito dispositivo o l&#39;identificatore con ambito piattaforma (presente nel payload SSO di Amazon) :

* Come intestazione : &quot;Token Adobe-Oggetto&quot;
* Come parametro di query : &quot;ast&quot;
* Come parametro post : &quot;ast&quot;


>[!NOTE]
>
>Se l’identificatore con ambito dispositivo o l’identificatore con ambito piattaforma viene inviato come parametro query/post, deve essere incluso durante la generazione della firma della richiesta.

>[!NOTE]
>
>Utilizzando il parametro di query &quot;ast&quot;, l&#39;intero url può diventare molto lungo e rifiutato. Nella chiamata /authenticate, questo parametro può essere ignorato come è stato fornito alla chiamata /regcode

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
>Se l&#39;SSO di Amazon non è presente o non è valido, l&#39;autenticazione di Adobe Primetime ignorerà l&#39;attributo e le chiamate verranno eseguite come se l&#39;SSO non fosse presente.
