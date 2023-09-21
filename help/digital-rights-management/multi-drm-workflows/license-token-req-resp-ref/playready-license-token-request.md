---
description: L'interfaccia del token di licenza PlayReady fornisce servizi di produzione e test.
title: Richiesta/risposta token di licenza PlayReady
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# Richiesta/risposta token di licenza PlayReady {#playready-license-token-request-response}

L&#39;interfaccia del token di licenza PlayReady fornisce servizi di produzione e test.

Questa richiesta HTTP restituisce un token che può essere riscattato per una licenza PlayReady.

**Metodo: GET, POST** (con un corpo codificato www-url contenente i parametri per entrambi i metodi)

**URL:**

* **Produzione:** `https://pr-gen.{prod_domain}/hms/pr/token`

* **Prova:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

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

## Parametri query richiesta {#section_26F8856641A64A46A3290DBE61ACFAD2}

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
   <td> <p>Questa è la chiave API del cliente, una per ogni ambiente di produzione e di test. È disponibile nella scheda ExpressPlay Admin Dashboard. </p> </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>o <span class="codeph"> html</span> o <span class="codeph"> json</span>. Se <span class="codeph"> html</span> (impostazione predefinita) nel corpo dell’entità della risposta viene fornita una rappresentazione HTML di eventuali errori. <p>Se <span class="codeph"> json</span> viene specificata, viene restituita una risposta strutturata in formato JSON. Consulta <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> Errori JSON</a> per i dettagli. </p> <p>Il tipo mime della risposta è <span class="codeph"> text/uri-list</span> al completamento, <span class="codeph"> text/html</span> per il formato di errore HTML, oppure <span class="codeph"> application/json</span> per il formato di errore JSON. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 10: Parametri di query della licenza**

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
   <td>Stringa esadecimale da 4 byte che rappresenta i flag di licenza. Deve essere impostato su "00000001" per una licenza persistente. <p>Nota: Licenze di noleggio (<span class="codeph"> rightsType=Noleggio</span>) DEVE essere persistente. </p> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> chiavetta</span> </td> 
   <td> Chiave di crittografia (KEK). Le chiavi vengono memorizzate crittografate con una chiave utilizzando un algoritmo di wrapping delle chiavi (Key Wrap di AES, RFC3394). </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> bambino</span> </td> 
   <td>Una rappresentazione di stringa esadecimale da 16 byte della chiave di crittografia del contenuto o di una stringa <span class="codeph"> ^somestring'</span>. La lunghezza della stringa seguita da '^' non può superare i 64 caratteri. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> Una rappresentazione di stringa esadecimale della chiave del contenuto crittografato. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> Una rappresentazione di stringa esadecimale da 16 byte della chiave di crittografia del contenuto </td> 
   <td>Sì, salvo <span class="codeph"> chiavetta</span> e <span class="codeph"> ek</span> o <span class="codeph"> bambino</span> sono fornite </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>Specifica il tipo di diritti. Deve essere <span class="codeph"> BuyToOwn</span> o <span class="codeph"> Affitto</span>. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.periodEndTime</span> </td> 
   <td>Data di fine noleggio. Questo valore DEVE essere nel formato "RFC 3339" _ data/ora nel formato "Z" dell’indicatore di zona ("Ora Zulu") o un numero intero preceduto da un segno "+". <p>Se il valore è un <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> formato data/ora, quindi rappresenta una data/ora di scadenza assoluta per la licenza. Un esempio di data/ora RFC 3339 è 2006-04-14T12:01:10Z </p> <p> Se il valore è un numero intero preceduto dal segno "+", viene considerato come un numero relativo di secondi dal momento in cui il token viene emesso. Il contenuto non può essere riprodotto in seguito. Valido solo se <span class="codeph"> rightsType</span> è <span class="codeph"> Affitto</span>. </p> </td> 
   <td>Sì, quando <span class="codeph"> rightsType</span> è <span class="codeph"> Affitto</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.playDuration</span> </td> 
   <td>Tempo, in secondi, in cui il contenuto può essere riprodotto una volta avviata la riproduzione. Valido solo se <span class="codeph"> rightsType</span> è Affitto. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogicoVideoOPL</span> </td> 
   <td> Valore intero per indicare il livello di protezione dell'uscita per il video analogico. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> Valore intero per indicare il livello di protezione dell'output per l'audio digitale compresso. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> Valore intero per indicare il livello di protezione dell'output per il video digitale compresso. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> Valore intero per indicare il livello di protezione dell'output per l'audio digitale non compresso. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalVideoOPL</span> </td> 
   <td> Valore intero per indicare il livello di protezione dell'output per il video digitale non compresso. Intervallo valido 0-999. </td> 
   <td> Sì </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>Comportamento richiesto quando l’output è sconosciuto. Valori consentiti: <span class="codeph"> Consenti</span>, <span class="codeph"> Non consentire</span> o <span class="codeph"> Solo SDO</span> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> Un valore esadecimale a 4 byte per indicare i flag per altre opzioni di controllo dell'output </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>Parola arbitraria di 4 lettere che rappresenta un identificatore a 32 bit per un'estensione. Il codice ASCII a 8 bit di ogni lettera è la porzione corrispondente a 8 bit dell'identificatore. Ad esempio, il valore dell’identificatore 0x61626364 (esadecimale) sarebbe scritto ‘<span class="codeph"> abcd</span>', perché il codice ASCII per 'a' è 0x61, ecc. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> Stringa con codifica base64 dell’estensione. </td> 
   <td>Sì, quando <span class="codeph"> extensionType</span> è specificato. </td> 
  </tr> 
 </tbody> 
</table>

## Risposte {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**Tabella 11: Risposte HTTP**

| **Codice di stato HTTP** | **Descrizione** | **Content-Type** | **Corpo entità contiene** |
|---|---|---|---|
| `200 OK` | Nessun errore. | `text/uri-list` | URL e token di acquisizione licenza |
| `400 Bad Request` | Argomenti non validi | `text/html` o `application/json` | Descrizione errore |
| `401 Unauthorized` | Autenticazione non riuscita | `text/html` o `application/json` | Descrizione errore |
| `404 Not found` | URL non valido | `text/html` o `application/json` | Descrizione errore |
| `50x Server Error` | Errore del server | `text/html` o `application/json` | Descrizione errore |

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
   <td>Token di autenticazione non valido: &lt;details&gt; <p>Nota: questo può accadere se l’autenticatore non è corretto o quando si accede all’API di test all’indirizzo *.test.expressplay.com utilizzando l’autenticatore di produzione e viceversa. </p> <p importance="high">Nota: Test SDK e Advanced Test Tool (ATT) funzionano solo con <span class="filepath"> *.test.expressplay.com</span>, che i dispositivi di produzione devono utilizzare <span class="filepath"> *.service.expressplay.com</span>. </p> </td> 
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
   <td><span class="codeph"> ContrassegnoControlloOutput</span> deve essere codificato di 4 byte </td> 
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
   <td> -4018 </td> 
   <td>Mancante <span class="codeph"> bambino</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Impossibile ottenere la chiave del contenuto dal servizio di archiviazione chiavi </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> bambino</span> deve contenere 32 caratteri esadecimali </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> bambino</span> deve contenere 64 caratteri dopo il simbolo ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>Non valido <span class="codeph"> bambino</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>Crittografia non valida <span class="codeph"> chiave</span> o kek </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> Errore di tipo di output sconosciuto non valido </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> Opzione PlayReady disabilitata per questo servizio </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Flag generali non validi </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> L'ID dispositivo deve contenere 32 caratteri esadecimali </td> 
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
   <td>Solo uno di <span class="codeph"> chiavetta</span> o <span class="codeph"> contentKey</span> può essere specificato </td> 
  </tr> 
 </tbody> 
</table>
