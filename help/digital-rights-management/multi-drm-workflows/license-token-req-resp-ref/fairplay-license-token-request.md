---
description: L'interfaccia del token di licenza FairPlay fornisce servizi di produzione e test.
seo-description: L'interfaccia del token di licenza FairPlay fornisce servizi di produzione e test.
seo-title: Richiesta/risposta token licenza FairPlay
title: Richiesta/risposta token licenza FairPlay
uuid: 10d4a760-8895-4fb3-8288-1c3a640df587
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 5%

---


# Richiesta e risposta del token di licenza FairPlay{#fairplay-license-token-request-response}

L&#39;interfaccia del token di licenza FairPlay fornisce servizi di produzione e test. Questa richiesta restituisce un token che può essere rimborsato per una licenza FairPlay.

**Metodo: GET, POST** (con un corpo codificato www-url che contiene parametri per entrambi i metodi)

**URL:**

* **Produzione:** `https://fp-gen.{prod_domain}/hms/fp/token`

* **Prova:** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **Richiesta di esempio:**

```<xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier> 
   &kid=<CEKSID> 
   &contentKey=<CEK> 
   &rightsType=BuyToOwn 
   &analogVideoOPL=0 
   &compressedDigitalAudioOPL=0 
   &compressedDigitalVideoOPL=0 
   &uncompressedDigitalAudioOPL=0 
   &uncompressedDigitalVideoOPL=0
```

* **Risposta di esempio:**

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

**Parametri query di richiesta**

**Tabella 3: Parametri query token**

| Parametro query | Descrizione | Obbligatorio |
|--- |--- |--- |
| customerAuthenticator Autenticator Autenticatore del cliente come parametro query customerAuthenticator FairPlay | Questa è la chiave API del cliente, una per ogni ambiente di produzione e di test. Potete trovarlo nella scheda ExpressPlay Admin Dashboard. | Yes |
| errorFormat | html o json. Se html (il valore predefinito) viene fornita una rappresentazione HTML di eventuali errori nel corpo dell&#39;entità della risposta. Se viene specificato json, viene restituita una risposta strutturata in formato JSON. Per ulteriori informazioni, vedere [Errori JSON](https://www.expressplay.com/developer/restapi/#json-errors). Il tipo mime della risposta è text/uri-list in caso di esito positivo, text/html per il formato di errore HTML o application/json per il formato di errore JSON. | No |

**Tabella 4: Parametri query licenza**

| **Parametro query** | **Descrizione** | **Obbligatorio** |
|---|---|---|
| `generalFlags` | Una stringa esadecimale a 4 byte che rappresenta i flag di licenza. &quot;0000&quot; è l&#39;unico valore consentito. | No |
| `kek` | Chiave di crittografia chiave (KEK). Le chiavi vengono memorizzate crittografate con un KEK che utilizza un algoritmo di wrapping delle chiavi (AES Key Wrap, RFC3394). Se viene fornito `kek`, è necessario specificare uno dei parametri `kid` o `ek`, *ma non entrambi*. | No |
| `kid` | Una stringa esadecimale a 16 byte che rappresenta la chiave di crittografia del contenuto o una stringa `'^somestring'`. La lunghezza della stringa seguita da `'^'` non può essere maggiore di 64 caratteri. | No |
| `ek` | Una rappresentazione stringa esadecimale della chiave di contenuto crittografata. | No |
| `contentKey` | Una rappresentazione di stringa esadecimale a 16 byte della chiave di crittografia del contenuto | Sì, a meno che non siano forniti `kek` e `ek` o `kid`. |
| `iv` | Una rappresentazione di stringa esadecimale a 16 byte della cifratura del contenuto IV | Yes |
| `rentalDuration` | Durata del noleggio in secondi (impostazione predefinita - 0) | No |
| `fpExtension` | Un modulo breve con wrapping `extensionType` e `extensionPayload` come stringa separata da virgola. Ad esempio: […] `&fpExtension=wudo,AAAAAA==&`[…] | No, è possibile utilizzare qualsiasi numero |

**Tabella 5: Parametri query limitazioni token**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Parametro query</b> </th> 
   <th class="entry"> <b>Descrizione</b> </th> 
   <th class="entry"> <b>Obbligatorio</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expiresTime  </span> </td> 
   <td> Tempo di scadenza del token. Questo valore DEVE essere una stringa in formato <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> data/ora nel designatore di zona "Z" ("Zulu time"), o un numero intero preceduto dal segno "+". Un esempio di data/ora RFC 3339 è <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>Se il valore è una stringa nel formato data/ora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a>, rappresenta una data/ora di scadenza assoluta per il token. Se il valore è un numero intero preceduto da un segno "+", viene interpretato come numero relativo di secondi, a partire dall'emissione, che il token è valido. </p> Ad esempio, <span class="codeph"> +60 </span> specifica un minuto. La durata massima e predefinita del token (se non specificata) è 30 giorni. </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 6: Parametri query di correlazione**

| **Parametro query** | **Descrizione** | **Obbligatorio** |
|---|---|---|
| `cookie` | Stringa arbitraria lunga fino a 32 caratteri, mantenuta nel token e registrata dal server di redenzione del token. Questo può essere utilizzato per correlare le voci di registro nel server di redenzione e quelle nei server del provider di servizi. | No |

**Risposta**

**Tabella 7: Risposte HTTP**

| **Codice di stato HTTP** | **Descrizione** | **Content-Type** | **Il corpo dell&#39;entità contiene** |
|---|---|---|---|
| `200 OK` | Nessun errore. | `text/uri-list` | URL acquisizione licenza + token |
| `400 Bad Request` | Argomenti non validi | `text/html` o  `application/json` | Descrizione errore |
| `401 Unauthorized` | Autenticazione non riuscita | `text/html` o  `application/json` | Descrizione errore |
| `404 Not found` | URL non valido | `text/html` o  `application/json` | Descrizione errore |
| `50x Server Error` | Errore del server | `text/html` o  `application/json` | Descrizione errore |

**Tabella 8: Codici di errore evento**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Code</b> </th> 
   <th class="entry"> <b>Descrizione</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> Scadenza token non valida: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> Indirizzo IP non valido </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> Chiave di crittografia del contenuto non valida: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> Sono stati specificati flag di controllo di output non validi: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> Il token di autenticazione deve essere fornito </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> Token di autenticazione non valido: &lt;details&gt; <p>Nota:  Ciò può accadere se l'autenticatore è errato o quando accede all'API test su <span class="filepath"> *.test.espressplay.com </span> utilizzando l'autenticatore di produzione e viceversa. </p> <p importance="high">Nota:  L'SDK test e lo strumento di test avanzato (ATT) funzionano solo con <span class="filepath"> *.test.espressplay.com </span>, mentre i dispositivi di produzione devono utilizzare <span class="filepath"> *.service.espressplay.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Token insufficienti </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> Tipo di diritti mancante </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> Tipo di diritti non valido </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> Ora di fine periodo di noleggio mancante </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> Durata della riproduzione a noleggio mancante </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> Durata di riproduzione noleggio non valida </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> La chiave di crittografia del contenuto deve contenere 32 cifre esadecimali </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> Errore Amministratore ExpressPlay: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> Account di servizio disattivato </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> cookie non valido </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> Controllo output non valido, valori non compresi nell'intervallo specificato </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> Nessun valore corrispondente specificato </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> Il tipo di estensione deve essere di 4 caratteri </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> Il payload dell'estensione deve essere codificato in Base64 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag  </span> deve essere codificato 4 byte </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> È stato specificato un formato di errore non valido: &lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> Impossibile autenticare il dispositivo </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> Token non valido </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> Kid mancante </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Impossibile ottenere la chiave del contenuto dal servizio di archiviazione chiavi </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> il ragazzo  </span> deve avere 32 caratteri esadecimali di lunghezza </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> il ragazzo  </span> deve avere 64 caratteri dopo il ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> Livello <span class="codeph"> </span> non valido </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> Chiave crittografata non valida o chiave <span class="codeph"> </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Flag generali non validi </td> 
  </tr> 
  <tr> 
   <td> -6001 </td> 
   <td> Parametri <span class="codeph"> FPExtax </span> non validi </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> Tipo token FP non valido </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> Parametro <span class="codeph"> iv </span> non valido specificato </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> Impossibile generare CKC per FP </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Dati chiave non validi specificati </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> Servizio non autorizzato per il supporto FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Durata noleggio specificata non valida </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> Il binding ID dispositivo non è supportato per FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> Opzione FairPlay disabilitata </td> 
  </tr> 
 </tbody> 
</table>