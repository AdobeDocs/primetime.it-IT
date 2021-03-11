---
description: L’interfaccia del token di licenza PlayReady fornisce servizi di produzione e test.
title: Richiesta/risposta token di licenza PlayReady
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---


# Richiesta/risposta del token di licenza PlayReady {#playready-license-token-request-response}

L’interfaccia del token di licenza PlayReady fornisce servizi di produzione e test.

Questa richiesta HTTP restituisce un token che può essere riscattato per una licenza PlayReady.

**Metodo: GET, POST**  (con un corpo codificato www-url-che contiene parametri per entrambi i metodi)

**URL:**

* **Produzione:** `https://pr-gen.{prod_domain}/hms/pr/token`

* **Test:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **Richiesta di esempio:**

   ```
   <xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
   https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator=
    <ExpressPlay customer authenticator identifier>
    &kid=<CEKSID>
    &contentKey=<CEK>
    &rightsType=BuyToOwn
    &analogVideoOPL=0
    &compressedDigitalAudioOPL=0
    &compressedDigitalVideoOPL=0
    &uncompressedDigitalAudioOPL=0
    &uncompressedDigitalVideoOPL=0
   </xref href="https:>
   ```

* **Risposta di esempio:**

   ```
   {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
               "token":"<base64-encoded ExpressPlay token>"}
   ```

## Parametri query di richiesta {#section_26F8856641A64A46A3290DBE61ACFAD2}

**Tabella 9: Parametri query token**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Parametro query</b> </th> 
   <th class="entry"><b>Descrizione</b> </th> 
   <th class="entry"><b>Obbligatorio</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>Questa è la chiave API del cliente, una per ogni ambiente di produzione e test. Puoi trovarlo nella scheda Dashboard di amministrazione di ExpressPlay. </p> </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>Oppure <span class="codeph"> html</span> o <span class="codeph"> json</span>. Se <span class="codeph"> html</span> (impostazione predefinita) nel corpo dell’entità della risposta viene fornita una rappresentazione HTML di eventuali errori. <p>Se è specificato <span class="codeph"> json</span>, viene restituita una risposta strutturata in formato JSON. Per ulteriori informazioni, consulta <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON Errors</a> . </p> <p>Il tipo mime della risposta è <span class="codeph"> text/uri-list</span> in caso di esito positivo, <span class="codeph"> text/html</span> per il formato di errore HTML o <span class="codeph"> application/json</span> per il formato di errore JSON. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 10: Parametri query di licenza**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Parametro query</b> </th> 
   <th class="entry"><b>Descrizione</b> </th> 
   <th class="entry"><b>Obbligatorio</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>Una stringa esadecimale a 4 byte che rappresenta i flag di licenza. Deve essere fissato a "00000001" per una licenza permanente. <p>Nota: Le licenze di noleggio (<span class="codeph"> rightsType=Rental</span>) DEVONO essere costanti. </p> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kek</span> </td> 
   <td> Chiave di crittografia (KEK). Le chiavi vengono memorizzate crittografate con un KEK utilizzando un algoritmo di wrapping chiave (AES Key Wrap, RFC3394). </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> bambino</span> </td> 
   <td>Una rappresentazione di stringa esadecimale a 16 byte della chiave di crittografia del contenuto o una stringa <span class="codeph"> ^somestring'</span>. La lunghezza della stringa seguita da '^' non può essere maggiore di 64 caratteri. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> Una rappresentazione stringa esadecimale della chiave di contenuto crittografata. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> Una rappresentazione di stringa esadecimale a 16 byte della chiave di crittografia del contenuto </td> 
   <td>Sì, a meno che non siano forniti <span class="codeph"> kek</span> e <span class="codeph"> ek</span> o <span class="codeph"> child</span> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>Specifica il tipo di diritti. Deve essere <span class="codeph"> BuyToOwn</span> o <span class="codeph"> Affitto</span>. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.periodEndTime</span> </td> 
   <td>Data di fine affitto. Questo valore DEVE essere nel formato "RFC 3339" _ data/ora nel formato "Z" zone designator ("Zulu time") o un numero intero preceduto dal segno "+". <p>Se il valore è un formato data/ora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a>, rappresenta una data/ora di scadenza assoluta per la licenza. Un esempio di RFC 3339 data/ora è 2006-04-14T12:01:10Z. </p> <p> Se il valore è un numero intero preceduto dal segno "+", viene preso come numero relativo di secondi dal momento in cui viene emesso il token. Il contenuto non può essere riprodotto dopo questo periodo di tempo. Valido solo se <span class="codeph"> rightsType</span> è <span class="codeph"> Affitto</span>. </p> </td> 
   <td>Sì, quando <span class="codeph"> rightsType</span> è <span class="codeph"> Affitto</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> noleggio.playDuration</span> </td> 
   <td>Tempo, in secondi, che il contenuto può essere riprodotto una volta avviata la riproduzione. Valido solo se <span class="codeph"> rightsType</span> è Affitto. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogicoVideoOPL</span> </td> 
   <td> Valore intero per indicare il Livello di protezione dell'uscita per il video analogico. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> Valore intero per indicare il Livello di protezione dell'output per l'audio digitale compresso. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressoDigitalVideoOPL</span> </td> 
   <td> Valore intero per indicare il Livello di protezione dell'output per il video digitale compresso. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> Valore intero per indicare il Livello di protezione dell'output per l'audio digitale non compresso. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> non compressoDigitalVideoOPL</span> </td> 
   <td> Valore intero per indicare il Livello di protezione dell'output per i video digitali non compressi. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>Comportamento richiesto quando l'output è sconosciuto. Valori consentiti: <span class="codeph"> Consenti</span>, <span class="codeph"> Non consentire</span> o <span class="codeph"> SDOnly</span> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> Un valore esadecimale a 4 byte per indicare i flag per altre opzioni di controllo dell'output </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>Una parola arbitraria di 4 lettere che rappresenta un identificatore a 32 bit per un'estensione. Il codice ASCII a 8 bit di ciascuna lettera corrisponde alla parte corrispondente a 8 bit byte dell'identificatore. Ad esempio, il valore dell'identificatore 0x61626364 (esadecimale) verrebbe scritto ‘<span class="codeph"> abcd</span>’, perché il codice ASCII per "a" è 0x61, ecc. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> Una stringa codificata base64 dell'estensione. </td> 
   <td>Sì, quando è specificato <span class="codeph"> extensionType</span>. </td> 
  </tr> 
 </tbody> 
</table>

## Risposte {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**Tabella 11: Risposte HTTP**

| **Codice di stato HTTP** | **Descrizione** | **Content-Type** | **Il corpo dell&#39;entità contiene** |
|---|---|---|---|
| `200 OK` | Nessun errore. | `text/uri-list` | URL e token di acquisizione della licenza |
| `400 Bad Request` | Archi non validi | `text/html` o  `application/json` | Descrizione errore |
| `401 Unauthorized` | Autenticazione non riuscita | `text/html` o  `application/json` | Descrizione errore |
| `404 Not found` | URL non valido | `text/html` o  `application/json` | Descrizione errore |
| `50x Server Error` | Errore del server | `text/html` o  `application/json` | Descrizione errore |

**Tabella 12: Codici di errore evento**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Codice</b> </th> 
   <th class="entry"><b>Descrizione</b> </th> 
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
   <td>Token di autenticazione non valido: &lt;details&gt; <p>Nota:  Questo può accadere se l'autenticatore è sbagliato o quando si accede all'API di test su *.test.espressplay.com utilizzando l'autenticatore di produzione e viceversa. </p> <p importance="high">Nota: L'SDK di test e lo strumento di test avanzato (ATT) funzionano solo con <span class="filepath"> *.test.espressplay.com</span>, mentre i dispositivi di produzione devono utilizzare <span class="filepath"> *.service.expression.play.com</span>. </p> </td> 
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
   <td><span class="codeph"> </span> OutputControlFlagdeve codificare 4 byte </td> 
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
   <td> -4018 </td> 
   <td>Mancante <span class="codeph"> figlio</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Impossibile ottenere la chiave di contenuto dal servizio di archiviazione chiavi </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> Il </span> rene deve essere lungo 32 caratteri esadecimali </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> </span> il bambino deve essere di 64 caratteri dopo il ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td><span class="codeph"> child</span> non valido </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>Chiave <span class="codeph"> crittografata </span> o chiave non valida </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> Errore del tipo di output sconosciuto non valido </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> L'opzione PlayReady è disabilitata per questo servizio </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Flag generali non validi </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> L'ID dispositivo deve essere lungo 32 caratteri esadecimali </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> ID dispositivo non valido </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> Valore OPL mancante </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>È possibile specificare solo uno dei <span class="codeph"> kek</span> o <span class="codeph"> contentKey</span> </td> 
  </tr> 
 </tbody> 
</table>
