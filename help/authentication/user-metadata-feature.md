---
title: Funzione metadati utente
description: Funzione metadati utente
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 0%

---



# Metadati utente {#user-metadata}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>
</br>

## Introduzione {#intro}

La funzione User Metadata consente ai programmatori di accedere a diversi tipi di dati specifici dell&#39;utente gestiti dagli MVPD.  I tipi di metadati utente includono codici postali, valutazioni parentali, ID utente e altro ancora.  *Utente* i metadati sono un’estensione ai *statico* metadati (token di autenticazione TTL, token di autorizzazione TTL e ID dispositivo).


Punti chiave metadati utente:

- Trasmesso all&#39;applicazione del programmatore durante i flussi di autenticazione e autorizzazione
- I valori vengono salvati nel token
- I valori possono essere normalizzati se diversi MVPD forniscono dati in formati diversi
- Alcuni parametri possono essere crittografati utilizzando la chiave del programmatore (ad esempio il codice postale)
- Valori specifici sono resi disponibili per Adobe tramite una modifica della configurazione

## Ottenimento dei metadati utente {#obtaining}

I metadati utente sono disponibili per i programmatori tramite AccessEnabler `getMetadata()` e tramite `/usermetadata` nell’API Clientless.  Per informazioni dettagliate sull’utilizzo di , consulta la documentazione API di Platform `getMetadata()` e il relativo callback `setMetadataStatus()` (o per gli endpoint e i parametri utilizzati nell&#39;API Clientless).

I programmatori ottengono i metadati fornendo una chiave per il tipo di metadati che desiderano ottenere: `getMetadata(key)`.  

I metadati vengono restituiti come segue: `setMetadataStatus(key, encrypted, data)`:

| Parametro | Tipo | Descrizione |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key` | Stringa | Specifica il tipo di metadati richiesti |
| `encrypted` | Booleano | Flag booleano che indica se il &quot;valore&quot; è crittografato o meno. Se questo è &quot;vero&quot;, allora &quot;valore&quot; sarà in realtà una rappresentazione JSON Web Encrypted del valore effettivo. |
| `data` | Oggetto | Un oggetto JSON contenente la rappresentazione dei metadati |

 

La struttura del parametro dati, i valori variano tra i tipi:

| Chiave | Tipo di valore | Esempio | Descrizione |
| --- | --- | --- | --- |
| `zip` | Array JSON | \[&quot;77754&quot;, &quot;12345&quot;\] | Codice postale |
| `householdID` | Stringa JSON | &quot;1o7241p&quot; | Identificatore della famiglia. Se l&#39;MVPD non supporta i sottoconti, sarà identico a `userID` |
| `maxRating` | Oggetto JSON | { MPAA: &quot;NR&quot;, <br>  VCHIP: &quot;X&quot;,  <br>  URL: &quot;http://manage.my/parental&quot; } | Valutazione massima dei genitori per l’utente |
| `userID` | Stringa JSON | &quot;1o7241p&quot; | Identificatore utente. Nel caso in cui un MVPD supporti i conti secondari e l&#39;utente non sia l&#39;account principale, `userID` sarà diverso da `householdID`. |
| `channelID` | Array JSON | \[&quot;channel-1&quot;, &quot;channel-2&quot; \] | Elenco dei canali autorizzati dall&#39;utente per la visualizzazione |
| `is_hoh` | Stringa JSON | &quot;1&quot; | Flag che identifica se un utente è il capo famiglia |
| `encryptedZip` | Stringa JSON | &quot;&quot; | Comcast espone il codice postale crittografato |
| `typeID` | Stringa JSON | Primaria | Flag che identifica se l’account utente è principale/secondario |
| `primaryOID` | Stringa JSON | &quot;uuidd1e19ec9-012c-124f-b520-acaf118d16a0&quot; | Identificatore della famiglia. Se `typeID` è primario, conterrà il valore del `userID` |
| hba_status | Booleano | &quot;true&quot; &quot;false&quot; | Flag booleano che indica se l’autenticazione basata su Home è abilitata per una particolare integrazione |
| allowMirroring | Booleano | &quot;true&quot; &quot;false&quot; | Indica se il mirroring dello schermo è consentito o meno per il dispositivo |

>[!NOTE]
>
> **Nota:** Se il parametro di dati è crittografato, come di solito accade per **zip**, la rappresentazione della chiave di metadati sarà una stringa JSON invece di un array o un oggetto.


**Importante:** I metadati utente effettivi disponibili per un programmatore dipendono da ciò che un MVPD rende disponibile.  Gli accordi legali devono essere firmati con gli MVPD prima di rendere disponibili nell&#39;ambiente di produzione i metadati utente sensibili (come ad esempio il codice zipcode).

</br>


| Nome | Dettagli | Richiede crittografia | Commenti |
| --- | --- | --- | --- |
| ID utente | Come fornito dall&#39;MVPD | No | Questo è il valore che viene poi hashing da Adobe ed esposto nel token multimediale e nel callback sendTrackingData() .<br><br>L&#39;hashing in questo caso è stato fatto per ragioni storiche<br><br>Questo ID può essere un ID di famiglia o un ID di account secondario. In genere non viene specificato, è solo l’ID associato all’accesso utilizzato al momento (che può essere un account principale o secondario) |
| ID utente a monte | Fornito dall&#39;MVPD da utilizzare solo per i flussi di monitoraggio della concorrenza | No | Questo valore viene utilizzato quando si applicano i limiti di concorrenza tra siti e app MVPD e Programmer. <br><br>L&#39;ID può contenere anche criteri di monitoraggio della concorrenza<br><br>Per la maggior parte degli MVPD questo valore è uguale all’ID utente |
| ID utente domestico | Fornito dall&#39;MVPD da utilizzare principalmente per i flussi di controllo dei genitori | No | ID che consente ai programmatori di comprendere l&#39;utilizzo di Household rispetto a Sub-account.<br><br>A volte viene utilizzato come sostituto di Controllo genitori se le valutazioni effettive non sono disponibili (se l’utente ha effettuato l’accesso con l’account della famiglia può controllare, altrimenti il contenuto valutato non verrà visualizzato)<br><br>C&#39;è molta varietà tra gli MVPD per come questo è rappresentato - ID utente domestico, capo di ID famiglia, testa di bandiera famiglia, ecc. |
| Capo famiglia | Segnalazione se il conto corrente è il capofamiglia o meno | No | vedi sopra |
| ID tipo / ID principale | Identificatori dei conti delle famiglie | No | Indicatori specifici AT&amp;T per il capo famiglia.<br><br>ID tipo = contrassegno che identifica se l’account utente è un account primario/secondario<br><br>OID principale = identificatore della famiglia. Se TypeID è primario, conterrà il valore dell&#39;ID utente |
| Valutazione massima | Valutazione massima consentita per il conto corrente | No | Consente ai programmatori di filtrare il contenuto non adatto per l’account.<br><br>Con valutazioni MPAA o VCHIP |
| Line-up dei canali | Elenco dei canali disponibili nel pacchetto dell’utente | No | Utilizzato per consentire/rimuovere rapidamente vari canali dai portali che aggregano più reti</br></br> *Si prega di notare che l&#39;autorizzazione di preflight generalmente consente una maggiore flessibilità per questo caso d&#39;uso e dovrebbe essere invece utilizzato* <br><br>La specifica OLCA consente questo come AttributeStatement nella risposta AuthN |
| Stato dell&#39;HBA | Indica se l&#39;autenticazione è stata eseguita tramite HBA | No |  |
| Codice postale | Codice postale di fatturazione dell’utente | Sì | Utilizzato per eventi broadcast o sportivi<br><br>Può essere fornito anche con la risposta AuthZ per aggiornamenti rapidi<br><br>Dati sensibili, necessita di accordi legali MVPD |
| Codice postale crittografato | Codice postale di fatturazione dell’utente (Comcast) | Sì | Come sopra ma criptato da Comcast |
| Lingua | Impostazioni della lingua utente | No | Utilizzato per visualizzare i messaggi in base alle preferenze dell&#39;utente |
| Consenti mirroring | Indica se il mirroring dello schermo è consentito o meno per il dispositivo | No |  |



## Metadati disponibili {#available_metadata}

La tabella seguente illustra lo stato corrente dei metadati utente nell’ecosistema di autenticazione Adobe Primetime:


|  | **Note legali **<br><br>**Accordo **<br><br>**Firmato (solo zip)** | **ID utente **<br><br>**su AuthN** | **Codice postale **<br><br>**su AuthN/Z** | **Valutazione **<br><br>**su AuthN/Z** | **Famiglia **<br><br>**ID su AuthN/Z** | **ID canale su AuthN** | **Capo di famiglia su AuthN** | **ID tipo su AuthN** | **OID principale su AuthN** | Lingua | UserID a monte **su AuthN** | Stato dell&#39;HBA | OnNet | inHome | Consenti mirroring su AuthZ | **Note** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Nome formale** | n/d | `userID` | `zip` | `maxRating` | `householdID` | `channelID` | is_hoh | typeID | primaryOID | language | upstreamUserID | hba_status | onNet | inHome | allowMirroring | 1. Per AuthN - È necessario modificare OiosamlMetadataParser in modo che tutti i parser abbiano abilitato questo nuovo attributo <br>2.  Per AuthZ - Non c&#39;è modo generico, perché l&#39;implementazione dell&#39;autorizzazione è specifica per MVPD |
| **Crittografia richiesta** | n/d | **No** | **Sì** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** |  |
| **Sensibile** | n/d | **No** | **Sì** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** |  |  |
| **IdP Adobe** | **Sì** | **Sì** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì** | **Sì** | **Sì** | **Sì** | **No** | **Sì** | **No** | **No** | **No** | **No** | Non è necessario alcun accordo legale. |
| **Synacor** | **Sì** | **Sì** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì** | **Sì** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** | **Accordo giuridico che non copre tutti gli MVPD proxy.**   <br>Questo è un supporto generico per Synacor - possibilmente non arrotolato a tutti i loro MVPD. |
| Piatto | **No** | **Sì** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** | Condivide lo stesso elenco di tutti gli MVPD di Synacor, più a monteUserID. |
| Comcast | **No** | **Sì** | **No** | **Sì (solo AuthZ)** | **Sì (solo AuthZ)** | **No** | **No** | **No** | **No** | **No** | **Sì** | **Sì** | **No** | **No** | **No** |  |
| **AT&amp;T** | **Sì** | **Sì** | **Sì (solo AuthN)** | **No** | **Sì (solo AuthN)** | **No** | **No** | **Sì** | **Sì** | **No** | **Sì** | **No** | **No** | **No** | **No** | Accordo legale firmato. |
| **Cablevision** | **Sì** | **Sì** | **Sì (solo AuthN)** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** | Accordo legale firmato. |
| **HTC** | **No** | **Sì** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| **Massilone proxy** | **Sì** | **Sì** | **Sì (solo AuthN)** | **No** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** | Accordo legale firmato. |
| **Clearleap Proxy** | **Sì** | **Sì** | **Sì (solo AuthN)** | **Sì (solo AuthZ)** | **No** | **No** | **No** | **No** | **No** | **Sì** | **Sì** | **No** | **No** | **No** | **No** | Accordo legale firmato. |
| Rogers | **No** | **Sì** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| RCN | **Sì** | **Sì** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| Carta | **Sì** | **Sì** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| Verizon | **No** | **Sì** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sì** | **Sì** | **No** | **No** | **No** |  |
| Eastlink | **No** | **Sì** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| GLDS proxy | **No** | **Sì** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| DTV | **Sì** | **Sì** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| COX | **No** | **Sì** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| Cogeco | **No** | **Sì** | **Sì (solo AuthN)** | **No** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** |  |
| Videotron | **No** | **Sì** | **Sì (solo AuthN)** | **No** | **Sì*** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** | Espone familyID con lo stesso valore di userID |
| Spettro | **Sì** | **Sì** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **Sì (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sì** | **Sì** | **No** | **No** | **Sì** |  |
| **Tutti gli altri **<br><br>**MVPD** | **No** | **Sì** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sì** | **No** | **No** | **No** | **No** | **Nessun accordo legale, metadati sensibili non disponibili per la produzione.**  <br>Per tutti gli MVPD, l&#39;ID utente è disponibile senza ulteriore lavoro. |


L’elenco dei tipi di metadati utente verrà esteso man mano che nuovi tipi saranno resi disponibili e aggiunti al sistema di autenticazione Adobe Primetime.

## Esempi di codice {#code_samples}

- [Esempio di codice 1](#code_sample1)
- [Esempio di codice 2 (Mock getMetadata)](#code_sample2)


### Esempio di codice 1 {#code_sample1}

```
    // Assuming a reference to the AccessEnabler has been previously obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if(status ==1) {
        // User is authenticated, request metadata
        ae.getMetadata("zip");
        ae.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if(encrypted) {
        // The metadata value is encrypted
        // Needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

### Esempio di codice 2 (Mock getMetadata) {#code_sample2}

```
    // Assuming a reference to the AccessEnabler has been
    //   previously obtained and stored in the "ae" variable
     
    // Mock the getMetadata() method
    var aeMock = {
        getMetadata: function(key) {
          var data = null;
          // Set mock data based on the received key,
          // according to the format in the spec
          switch(key) {
            case 'zip': 
              data = [ "1235", "23456" ];
              break;
            case 'maxRating': 
              data = { "MPAA": "PG-13", "VCHIP": "TV-14" };
              break;
            default:
              break;
          }
          // Call the metadata status just like AccessEnabler does
          setMetadataStatus(key, false, data);
        }
     }
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if (status == 1) {
        // User is authenticated, request metadata using mock object
        aeMock.getMetadata("zip");
        aeMock.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the  setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if (encrypted) {
        // The metadata value is encrypted, so it
        //   needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

Per informazioni dettagliate sulla piattaforma in uso o per ottenere informazioni sull&#39;elaborazione dei metadati utente sul lato MVPD, consulta il collegamento appropriato in Informazioni correlate di seguito.  

<!---

## Related Information {#related}

- ActionScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- JavaScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- iOS - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaStatus)
- Android - [getMetadata()](#getMetadata), [setMetadataStatus()](#setMetadaStatus)
- Clientless - [AuthN Metadata](#authn_metadata)
- [MVPD Integration Guide: User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
-->
