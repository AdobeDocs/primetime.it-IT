---
description: Lavora con il SEES per vedere come abilitare un servizio di adesione basato su tempo utilizzando ExpressPlay.
title: Autorizzazione basata sul tempo del servizio di riferimento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# Servizio di riferimento: Adesione basata sul tempo {#reference-service-time-based-entitlement}

Lavora con il SEES per vedere come abilitare un servizio di adesione basato su tempo utilizzando ExpressPlay.

Il SEES riceve una richiesta di adesione (consulta la sezione API pubblica ) dal client. Il server SEES cerca i CEK e IV in base al `contentID`, aggiunge il `expirationTime` e inoltra la richiesta al server ExpressPlay. Il token ExpressPlay finale è vincolato al tempo. Vedi il diagramma della sequenza di titolarità basata sul tempo qui sotto. ![](assets/fees-time-based.png)

**Tabella 1: Parametri di licenza inviati dal client**

| Parametro query | Descrizione | Obbligatorio |
|---|---|---|
| `contentKey` | Una rappresentazione di stringa esadecimale a 16 byte della chiave di crittografia del contenuto | Sì |
| `iv` | Una rappresentazione di stringa esadecimale a 16 byte della crittografia del contenuto IV | Sì |
| `rentalDuration` | Durata del noleggio in secondi (valore predefinito = 0) | No |

**Tabella 2: Parametri di restrizione token aggiunti dal server SEES**

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
   <td>Tempo di scadenza del token. Questo valore deve essere una stringa in formato data/ora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> nel designatore di zona Z ("ora Zulu") o un numero intero preceduto dal segno '+'. Un esempio di RFC 3339 date/ora è <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>Se il valore è una stringa in formato data/ora RFC 339, rappresenta una data/ora di scadenza assoluta per il token. Se il valore è un numero intero preceduto dal segno "+", viene interpretato come un numero relativo di secondi dall'emissione per cui il token è valido. Ad esempio, <span class="codeph"> +60</span> specifica un minuto. La durata massima (e predefinita, se non specificata) del token è di 30 giorni. Utilizzare il modulo codificato "%2B" quando si specifica il segno "+". </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

