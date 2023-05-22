---
description: L'interfaccia dei token di licenza FairPlay fornisce servizi di produzione e test.
title: Richiesta/risposta token di licenza FairPlay
exl-id: 7073a74b-d907-4d45-8550-4305655c33f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 4%

---

# Richiesta e risposta del token di licenza FairPlay {#fairplay-license-token-request-response}

L&#39;interfaccia dei token di licenza FairPlay fornisce servizi di produzione e test. Questa richiesta restituisce un token che può essere riscattato per una licenza FairPlay.

**Metodo: GET, POST** (con un corpo codificato www-url contenente i parametri per entrambi i metodi)

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

**Parametri query richiesta**

**Tabella 3: Parametri query token**

| Parametro query | Descrizione | Obbligatorio |
|--- |--- |--- |
| customerAuthenticator Autenticatore del cliente come parametro di query customerAuthenticator FairPlay | Questa è la chiave API del cliente, una per ogni ambiente di produzione e di test. È disponibile nella scheda ExpressPlay Admin Dashboard. | Sì |
| errorFormat | html o json. Se html (l’impostazione predefinita), nel corpo dell’entità della risposta viene fornita una rappresentazione HTML di eventuali errori. Se si specifica json, viene restituita una risposta strutturata in formato JSON. Consulta [Errori JSON](https://www.expressplay.com/developer/restapi/#json-errors) per i dettagli. Il tipo mime della risposta è text/uri-list on success, text/html for HTML error format o application/json for JSON error format. | No |

**Tabella 4: Parametri di query della licenza**

| **Parametro query** | **Descrizione** | **Obbligatorio** |
|---|---|---|
| `generalFlags` | Stringa esadecimale da 4 byte che rappresenta i flag di licenza. &quot;0000&quot; è l’unico valore consentito. | No |
| `kek` | Chiave di crittografia (KEK). Le chiavi vengono memorizzate crittografate con una chiave utilizzando un algoritmo di wrapping delle chiavi (Key Wrap di AES, RFC3394). Se `kek` viene fornito, uno dei `kid` o `ek` parametri da fornire, *ma non entrambi*. | No |
| `kid` | Una rappresentazione di stringa esadecimale da 16 byte della chiave di crittografia del contenuto o di una stringa `'^somestring'`. La lunghezza della stringa seguita dalla stringa `'^'` non può superare i 64 caratteri. | No |
| `ek` | Una rappresentazione di stringa esadecimale della chiave del contenuto crittografato. | No |
| `contentKey` | Una rappresentazione di stringa esadecimale da 16 byte della chiave di crittografia del contenuto | Sì, a meno che `kek` e `ek` o `kid` vengono fornite. |
| `iv` | Una rappresentazione di stringa esadecimale da 16 byte della crittografia del contenuto IV | Sì |
| `rentalDuration` | Durata del noleggio in secondi (impostazione predefinita - 0) | No |
| `fpExtension` | Ritorno a capo in forma breve `extensionType` e `extensionPayload`, come stringa separata da virgole. Ad esempio: [...] `&fpExtension=wudo,AAAAAA==&`[...] | No, è possibile utilizzare qualsiasi numero |

**Tabella 5: Parametri query di restrizione token**

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
   <td> <span class="codeph"> expirationTime </span> </td> 
   <td> Data di scadenza del token. Questo valore DEVE essere una stringa in <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> formato data/ora nel designatore di zona "Z" ("Ora Zulu") o un numero intero preceduto dal segno "+". Un esempio di data/ora RFC 3339 è <span class="codeph"> 04-04-2006:01:10Z </span>. <p>Se il valore è una stringa in <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> formato data/ora, quindi rappresenta una data/ora di scadenza assoluta del token. Se il valore è un numero intero preceduto dal segno "+", viene interpretato come un numero relativo di secondi, dall’emissione, di validità del token. </p> Ad esempio: <span class="codeph"> +60 </span> specifica un minuto. La durata massima e predefinita del token (se non specificata) è di 30 giorni. </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 6: Parametri della query di correlazione**

| **Parametro query** | **Descrizione** | **Obbligatorio** |
|---|---|---|
| `cookie` | Stringa arbitraria lunga fino a 32 caratteri, inserita nel token e registrata dal server di rimborso del token. Può essere utilizzato per correlare le voci di registro nel server di riscatto e quelle nei server del provider di servizi. | No |

**Risposta**

**Tabella 7: Risposte HTTP**

| **Codice di stato HTTP** | **Descrizione** | **Content-Type** | **Corpo entità contiene** |
|---|---|---|---|
| `200 OK` | Nessun errore. | `text/uri-list` | URL di acquisizione licenza + token |
| `400 Bad Request` | Argomenti non validi | `text/html` o `application/json` | Descrizione errore |
| `401 Unauthorized` | Autenticazione non riuscita | `text/html` o `application/json` | Descrizione errore |
| `404 Not found` | URL non valido | `text/html` o `application/json` | Descrizione errore |
| `50x Server Error` | Errore del server | `text/html` o `application/json` | Descrizione errore |

**Tabella 8: Codici di errore evento**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Codice</b> </th> 
   <th class="entry"> <b>Descrizione</b> </th> 
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
   <td> Token di autenticazione non valido: &lt;details&gt; <p>Nota: questo può accadere se l’autenticatore ha torto o quando si accede all’API di test in <span class="filepath"> *.test.expressplay.com </span> utilizzando l’autenticatore di produzione e viceversa. </p> <p importance="high">Nota: Test SDK e Advanced Test Tool (ATT) funzionano solo con <span class="filepath"> *.test.expressplay.com </span>, che i dispositivi di produzione devono utilizzare <span class="filepath"> *.service.expressplay.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Numero insufficiente di token disponibili </td> 
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
   <td> Figlio mancante </td> 
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
   <td> <span class="codeph"> bambino </span> deve contenere 64 caratteri dopo il simbolo ^ </td> 
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
   <td> -6001 </td> 
   <td> Non valido <span class="codeph"> FPExtension </span> parametri specificati </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> Tipo di token FP non valido </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> Non valido <span class="codeph"> iv </span> parametro specificato </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> Impossibile generare CKC per FP </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Dati chiave specificati non validi </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> Servizio non autorizzato per il supporto FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Durata noleggio non valida specificata </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> Associazione ID dispositivo non supportata per FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> Opzione FairPlay disabilitata </td> 
  </tr> 
 </tbody> 
</table>
