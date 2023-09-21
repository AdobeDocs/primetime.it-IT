---
description: Lavora con il SEES per scoprire come abilitare un servizio di adesione basato sul tempo utilizzando ExpressPlay.
title: Autorizzazione basata su tempo del servizio di riferimento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Servizio di riferimento: diritto basato sul tempo {#reference-service-time-based-entitlement}

Lavora con il SEES per scoprire come abilitare un servizio di adesione basato sul tempo utilizzando ExpressPlay.

Il SEES riceve una richiesta di adesione (consulta la sezione API pubblica) dal client. Il server SEES cerca i valori CEK e IV in base al `contentID`, aggiunge `expirationTime`e inoltra la richiesta al server ExpressPlay. Il token ExpressPlay finale è vincolato al tempo. Vedere il diagramma della sequenza di diritti basati sul tempo riportato di seguito. ![](assets/fees-time-based.png)

**Tabella 1: Parametri di licenza inviati dal client**

| Parametro query | Descrizione | Obbligatorio |
|---|---|---|
| `contentKey` | Una rappresentazione di stringa esadecimale da 16 byte della chiave di crittografia del contenuto | Sì |
| `iv` | Una rappresentazione di stringa esadecimale da 16 byte della crittografia del contenuto IV | Sì |
| `rentalDuration` | Durata del noleggio in secondi (impostazione predefinita = 0) | No |

**Tabella 2: Parametri di restrizione dei token aggiunti dal server SEES**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> Parametro query </th> 
   <th class="entry"> Descrizione </th> 
   <th class="entry"> Obbligatorio </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>Data di scadenza del token. Questo valore deve essere una stringa in <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> formato data/ora nell'indicatore di zona 'Z' ("Ora Zulu") o un numero intero preceduto da un segno '+'. Un esempio di data/ora RFC 3339 è <span class="codeph"> 04-04-2006:01:10Z</span>. <p>Se il valore è una stringa nel formato data/ora RFC 3339, rappresenta una data/ora di scadenza assoluta per il token. Se il valore è un numero intero preceduto dal segno "+", viene interpretato come un numero relativo di secondi dall’emissione per cui il token è valido. Ad esempio: <span class="codeph"> +60</span> specifica un minuto. La durata massima del token (e predefinita, se non specificata) è di 30 giorni. Utilizzare il modulo codificato "%2B" quando si specifica il segno "+". </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>
