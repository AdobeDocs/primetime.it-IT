---
description: L’interfaccia del token di licenza Widevine fornisce servizi di produzione e test.
title: Richiesta/risposta token di licenza Widevine
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---


# Richiesta token di licenza Widevine / risposta {#widevine-license-token-request-response}

L’interfaccia del token di licenza Widevine fornisce servizi di produzione e test.

Questa richiesta HTTP restituisce un token che può essere riscattato per una licenza Widevine.

**Metodo: GET, POST**  (con un corpo codificato www-url-che contiene parametri per entrambi i metodi)

**URL:**

* **Produzione:** `https://wv-gen.{prod_domain}/hms/wv/token`

* **Test:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **Richiesta di esempio:**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **Risposta di esempio:**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**Tabella 13: Parametri query token**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Parametro query</b> </th> 
   <th class="entry"> <b>Descrizione</b> </th> 
   <th class="entry"> <b>Obbligatorio</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator  </span> </td> 
   <td> <p>Questa è la chiave API del cliente, una per ogni ambiente di produzione e test. Puoi trovarlo nella scheda Dashboard di amministrazione di ExpressPlay. </p> </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat  </span> </td> 
   <td> Oppure <span class="codeph"> html </span> o <span class="codeph"> json </span>. <p>Se <span class="codeph"> html </span> (impostazione predefinita) viene fornita una rappresentazione HTML di eventuali errori nel corpo dell’entità della risposta. Se è specificato <span class="codeph"> json </span>, viene restituita una risposta strutturata in formato JSON. Per ulteriori informazioni, consulta <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> Errori JSON </a> . </p> <p>Il tipo mime della risposta è <span class="codeph"> text/uri-list </span> in caso di esito positivo, <span class="codeph"> text/html </span> per il formato di errore <span class="codeph"> html </span> o <span class="codeph"> application/json </span> per il formato di errore <span class="codeph"> json </span>. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 14: Parametri query di licenza**

| Parametro query | Descrizione | Obbligatorio |
|--- |--- |--- |
| `generalFlags` | Una stringa esadecimale a 4 byte che rappresenta i flag di licenza. &quot;0000&quot; è l’unico valore consentito | No |
| `kek` | Chiave di crittografia (KEK). Le chiavi vengono memorizzate crittografate con un KEK utilizzando un algoritmo di wrapping chiave (AES Key Wrap, RFC3394). | No |
| `kid` | Una rappresentazione di stringa esadecimale a 16 byte della chiave di crittografia del contenuto o una stringa `^somestring'`. La lunghezza della stringa seguita da `^` non può essere maggiore di 64 caratteri. Per un esempio, controlla la nota qui sotto. | Sì |
| `ek` | Una rappresentazione stringa esadecimale della chiave di contenuto crittografata. | No |
| `contentKey` | Una rappresentazione di stringa esadecimale a 16 byte della chiave di crittografia del contenuto | Sì, a meno che non siano forniti `kek` e `ek` o `kid` |
| `contentId` | Id Contenuto | No |
| `securityLevel` | I valori consentiti sono da 1 a 5. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | Sì |
| `hdcpOutputControl` | I valori consentiti sono 0, 1, 2. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | Sì |
| `licenseDuration` * | Durata della licenza in secondi. Se non viene fornito, indica che non vi è alcun limite alla durata. Si prega di controllare la nota qui sotto per informazioni dettagliate. | No |
| `wvExtension` | Un oggetto extensionType e extensionPayload a forma breve, come stringa separata da virgole. Vedere il formato di seguito. Esempio: `…&wvExtension=wudo,AAAAAA==&…` | No, è possibile utilizzare qualsiasi numero |

Informazioni su `licenseDuration`: <ol><li> La riproduzione si interrompe `licenseDuration` secondi dopo l&#39;inizio della riproduzione. </li><li> Per consentire l&#39;arresto/la ripresa della riproduzione per un periodo di tempo illimitato, omettere `licenseDuration` (per impostazione predefinita, sarà infinito). In caso contrario, specificare il periodo di tempo durante il quale gli utenti finali dovrebbero essere in grado di godere del flusso. </li></ol>

**Tabella 15: Parametri query di limitazione token**

| Parametro query | Descrizione | Obbligatorio |
|--- |--- |--- |
| `expirationTime` | Tempo di scadenza del token. Questo valore DEVE essere una stringa nel formato [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) data/ora nel designatore di zona Z (&quot;ora Zulu&quot;) o un numero intero preceduto dal segno +. Un esempio di RFC 3339 data/ora è 2006-04-14T12:01:10Z. <br> Se il valore è una stringa in formato data/ora  [RFC 339](https://www.ietf.org/rfc/rfc3339.txt) , rappresenta una data/ora di scadenza assoluta per il token. Se il valore è un numero intero preceduto da un segno +, viene interpretato come un numero relativo di secondi, a partire dall&#39;emissione, che il token è valido. Ad esempio, `+60` specifica un minuto. <br> La durata massima e predefinita del token (se non specificata) è di 30 giorni. | No |

**Tabella 16: Parametri query di correlazione**

| **Parametro query** | **Descrizione** | **Obbligatorio** |
|---|---|---|
| `cookie` | Stringa arbitraria lunga fino a 32 caratteri mantenuta nel token e registrata dal server di rimborso del token. Può essere utilizzato per correlare le voci di registro nel server di rimborso e quelle nei server del provider di servizi. | No |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**Tabella 17: Risposta HTTP**

| **Codice di stato HTTP** | **Descrizione** | **Content-Type** | **Il corpo dell&#39;entità contiene** |
|---|---|---|---|
| `200 OK` | Nessun errore. | `text/uri-list` | URL di acquisizione della licenza + token |
| `400 Bad Request` | Archi non validi | `text/html` o  `application/json` | Descrizione errore |
| `401 Unauthorized` | Autenticazione non riuscita | `text/html` o  `application/json` | Descrizione errore |
| `404 Not found` | URL non valido | `text/html` o  `application/json` | Descrizione errore |
| `50x Server Error` | Errore del server | `text/html` o  `application/json` | Descrizione errore |

**Tabella 18: Codici di errore evento**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> Codice </th> 
   <th class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> Data di scadenza token non valida: &lt;details&gt; </td> 
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
   <td> Flag di controllo di output specificati non validi: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> Il token di autenticazione deve essere fornito </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> Token di autenticazione non valido: &lt;details&gt; <p>Nota:  Questo può accadere se l'autenticatore è sbagliato o quando si accede all'API di test su *.test.espressplay.com utilizzando l'autenticatore di produzione e viceversa. </p> <p importance="high">Nota:  L'SDK di test e lo strumento di test avanzato (ATT) funzionano solo con <span class="filepath"> *.test.espressplay.com </span>, mentre i dispositivi di produzione devono utilizzare <span class="filepath"> *.service.expression.play.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Token insufficienti </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> Ora di fine periodo del noleggio mancante </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> Durata di gioco a noleggio mancante </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> Durata della riproduzione a noleggio non valida </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> La chiave di crittografia del contenuto deve essere lunga 32 cifre esadecimali </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> Errore amministratore di ExpressPlay: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> Account di servizio disattivato </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> Cookie non valido </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> Controllo di output non valido. Valori non compresi nell'intervallo specificato </td> 
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
   <td> Il payload dell’estensione deve essere codificato in Base64 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag  </span> deve essere codificato 4 byte </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> Formato di errore specificato non valido: &lt;format&gt; </td> 
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
   <td> Elemento <span class="filepath"> mancante </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Impossibile ottenere la chiave di contenuto dal servizio di archiviazione chiavi </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> il bambino  </span> deve essere lungo 32 caratteri esadecimali </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> il bambino  </span> deve essere lungo 64 caratteri dopo il '^' </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> Elemento <span class="codeph"> non valido </span> </td> 
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
   <td> -6005 </td> 
   <td> Dati chiave non validi specificati </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Durata di noleggio non valida specificata </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> Il binding ID dispositivo non è supportato per Widevine </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> Valore livello di protezione mancante </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> Valore del livello di protezione non valido </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> Valore di controllo dell'uscita HDCP mancante </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> Durata licenza non valida specificata </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> Impossibile generare la licenza Widevine </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> Parametri <span class="codeph"> WVExtension </span> non validi specificati </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Opzione Widevine disabilitata </td> 
  </tr> 
 </tbody> 
</table>