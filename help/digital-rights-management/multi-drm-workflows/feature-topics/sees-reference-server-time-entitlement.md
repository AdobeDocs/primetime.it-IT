---
description: Utilizzate SEES per vedere come abilitare un servizio di adesione basato su tempo utilizzando ExpressPlay.
seo-description: Utilizzate SEES per vedere come abilitare un servizio di adesione basato su tempo utilizzando ExpressPlay.
seo-title: Adesione basata su tempo del servizio di riferimento
title: Adesione basata su tempo del servizio di riferimento
uuid: dd937299-a271-49a9-9b26-eec16f1484df
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Servizio di riferimento: Adesione basata su tempo {#reference-service-time-based-entitlement}

Utilizzate SEES per vedere come abilitare un servizio di adesione basato su tempo utilizzando ExpressPlay.

Il SEES riceve una richiesta di adesione (consultate la sezione API pubblica) dal client. Il server SEES cerca CEK e IV in base al `contentID`, aggiunge il `expirationTime` e inoltra la richiesta al server ExpressPlay. Il token ExpressPlay finale è vincolato dal tempo. Consultate il diagramma della sequenza Adesione basata su tempo riportato di seguito. ![](assets/fees-time-based.png)

**Tabella 1: Parametri di licenza inviati dal client**

| Parametro query | Descrizione | Obbligatorio |
|---|---|---|
| `contentKey` | Una rappresentazione di stringa esadecimale a 16 byte della chiave di crittografia del contenuto | Yes |
| `iv` | Una rappresentazione di stringa esadecimale a 16 byte della cifratura del contenuto IV | Yes |
| `rentalDuration` | Durata del noleggio in secondi (impostazione predefinita = 0) | No |

**Tabella 2: Parametri di limitazione token aggiunti dal server SEES**

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
   <td><span class="codeph"> expiresTime</span> </td> 
   <td>Tempo di scadenza del token. Questo valore deve essere una stringa nel formato data/ora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> nel designatore di zona "Z" ("Zulu time") o un numero intero preceduto dal segno "+". Un esempio di data/ora RFC 3339 è <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>Se il valore è una stringa in formato data/ora RFC 3339, rappresenta una data/ora di scadenza assoluta per il token. Se il valore è un numero intero preceduto dal segno "+", viene interpretato come un numero relativo di secondi dall'emissione per indicare che il token è valido. Ad esempio, <span class="codeph"> +60</span> specifica un minuto. La durata massima (e predefinita, se non specificata) del token è 30 giorni. Utilizzare il modulo codificato "%2B" quando si specifica il segno "+". </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

