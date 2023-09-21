---
description: L'interfaccia dei token di licenza di Widevine fornisce servizi di produzione e test.
title: Richiesta/risposta token di licenza widevine
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---

# Richiesta/risposta token di licenza widevine {#widevine-license-token-request-response}

L&#39;interfaccia dei token di licenza di Widevine fornisce servizi di produzione e test.

Questa richiesta HTTP restituisce un token che può essere riscattato per una licenza Widevine.

**Metodo: GET, POST** (con un corpo codificato www-url contenente i parametri per entrambi i metodi)

**URL:**

* **Produzione:** `https://wv-gen.{prod_domain}/hms/wv/token`

* **Prova:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

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
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>Questa è la chiave API del cliente, una per ogni ambiente di produzione e di test. È disponibile nella scheda ExpressPlay Admin Dashboard. </p> </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat </span> </td> 
   <td> o <span class="codeph"> html </span> o <span class="codeph"> json </span>. <p>Se <span class="codeph"> html </span> (impostazione predefinita) nel corpo dell’entità della risposta viene fornita una rappresentazione HTML di eventuali errori. Se <span class="codeph"> json </span> viene specificata, viene restituita una risposta strutturata in formato JSON. Consulta <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> Errori JSON </a> per i dettagli. </p> <p>Il tipo mime della risposta è <span class="codeph"> text/uri-list </span> al completamento, <span class="codeph"> text/html </span> per <span class="codeph"> html </span> formato dell’errore, oppure <span class="codeph"> application/json </span> per <span class="codeph"> json </span> formato dell’errore. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 14: Parametri di query della licenza**

| Parametro query | Descrizione | Obbligatorio |
|--- |--- |--- |
| `generalFlags` | Stringa esadecimale da 4 byte che rappresenta i flag di licenza. &quot;0000&quot; è l’unico valore consentito | No |
| `kek` | Chiave di crittografia (KEK). Le chiavi vengono memorizzate crittografate con una chiave utilizzando un algoritmo di wrapping delle chiavi (Key Wrap di AES, RFC3394). | No |
| `kid` | Una rappresentazione di stringa esadecimale da 16 byte della chiave di crittografia del contenuto o di una stringa `^somestring'`. La lunghezza della stringa seguita dalla stringa `^` non può superare i 64 caratteri. Per un esempio, consulta la nota seguente. | Sì |
| `ek` | Una rappresentazione di stringa esadecimale della chiave del contenuto crittografato. | No |
| `contentKey` | Una rappresentazione di stringa esadecimale da 16 byte della chiave di crittografia del contenuto | Sì, salvo `kek` e `ek` o `kid` sono fornite |
| `contentId` | ID contenuto | No |
| `securityLevel` | I valori consentiti sono 1-5. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | Sì |
| `hdcpOutputControl` | I valori consentiti sono 0, 1, 2. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | Sì |
| `licenseDuration` * | Durata della licenza in secondi. Se non specificato, indica che non vi è alcun limite alla durata. Per informazioni dettagliate, consulta la nota seguente. | No |
| `wvExtension` | Un breve modulo che racchiude extensionType ed extensionPayload, sotto forma di stringa separata da virgole. Vedi il formato di seguito. Esempio: `…&wvExtension=wudo,AAAAAA==&…` | No, è possibile utilizzare qualsiasi numero |

Informazioni su `licenseDuration`: <ol><li> La riproduzione si interrompe `licenseDuration` secondi dopo l’inizio della riproduzione. </li><li> Per consentire l&#39;interruzione o la ripresa della riproduzione per un periodo di tempo illimitato, omettere `licenseDuration` (il valore predefinito è infinite). In caso contrario, specifica la quantità di tempo durante la quale gli utenti finali dovrebbero essere in grado di fruire del flusso. </li></ol>

**Tabella 15: Parametri query di restrizione token**

| Parametro query | Descrizione | Obbligatorio |
|--- |--- |--- |
| `expirationTime` | Data di scadenza del token. Questo valore DEVE essere una stringa in [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) formato data/ora nel designatore di zona &quot;Z&quot; (&quot;Ora Zulu&quot;) o un numero intero preceduto da un segno +. Un esempio di data/ora RFC 3339 è 2006-04-14T12:01:10Z <br> Se il valore è una stringa in [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) formato data/ora, quindi rappresenta una data/ora di scadenza assoluta del token. Se il valore è un numero intero preceduto dal segno +, viene interpretato come un numero relativo di secondi, a partire dall’emissione, di validità del token. Ad esempio: `+60` specifica un minuto. <br> La durata massima e predefinita del token (se non specificata) è di 30 giorni. | No |

**Tabella 16: Parametri della query di correlazione**

| **Parametro query** | **Descrizione** | **Obbligatorio** |
|---|---|---|
| `cookie` | Stringa arbitraria contenente fino a 32 caratteri nel token e registrata dal server di recupero dei token. Può essere utilizzato per correlare le voci di registro nel server di rimborso e quelle nei server del provider di servizi. | No |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**Tabella 17: Risposta HTTP**

| **Codice di stato HTTP** | **Descrizione** | **Content-Type** | **Corpo entità contiene** |
|---|---|---|---|
| `200 OK` | Nessun errore. | `text/uri-list` | URL di acquisizione licenza + token |
| `400 Bad Request` | Argomenti non validi | `text/html` o `application/json` | Descrizione errore |
| `401 Unauthorized` | Autenticazione non riuscita | `text/html` o `application/json` | Descrizione errore |
| `404 Not found` | URL non valido | `text/html` o `application/json` | Descrizione errore |
| `50x Server Error` | Errore del server | `text/html` o `application/json` | Descrizione errore |

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
   <td> Data di scadenza del token non valida: &lt;details&gt; </td> 
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
   <td> È necessario fornire il token di autenticazione </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> Token di autenticazione non valido: &lt;details&gt; <p>Nota: questo può accadere se l’autenticatore non è corretto o quando si accede all’API di test all’indirizzo *.test.expressplay.com utilizzando l’autenticatore di produzione e viceversa. </p> <p importance="high">Nota: Test SDK e Advanced Test Tool (ATT) funzionano solo con <span class="filepath"> *.test.expressplay.com </span>, che i dispositivi di produzione devono utilizzare <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Numero insufficiente di token disponibili </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> Ora di fine periodo di noleggio mancante </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> Durata riproduzione in affitto mancante </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> Durata riproduzione in affitto non valida </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> La chiave di crittografia del contenuto deve contenere 32 cifre esadecimali </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> Errore di amministrazione di ExpressPlay: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> Account del servizio disabilitato </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> Cookie non valido </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> Controllo di output non valido, valori non compresi nell'intervallo specificato </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> Nessun valore corrispondente specificato </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> Il tipo di estensione può contenere un massimo di 4 caratteri </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> Il payload dell’estensione deve essere codificato in Base64 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> ContrassegnoControlloOutput </span> deve essere codificato di 4 byte </td> 
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
   <td> Mancante <span class="filepath"> bambino </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Impossibile ottenere la chiave del contenuto dal servizio di archiviazione chiavi </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> bambino </span> deve contenere 32 caratteri esadecimali </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> bambino </span> deve contenere 64 caratteri dopo '^' </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> Non valido <span class="codeph"> bambino </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> Chiave crittografata non valida o <span class="codeph"> chiavetta </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Flag generali non validi </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Dati chiave specificati non validi </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Durata noleggio non valida specificata </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> L'associazione ID dispositivo non è supportata per Widevine </td> 
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
   <td> Valore di controllo uscita HDCP mancante </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> Durata licenza non valida </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> Impossibile generare la licenza Widevine </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> Non valido <span class="codeph"> Estensione WVE </span> parametri specificati </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Opzione widevine disabilitata </td> 
  </tr> 
 </tbody> 
</table>
