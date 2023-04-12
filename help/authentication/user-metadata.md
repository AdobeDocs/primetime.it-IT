---
title: Metadati utente
description: Metadati utente
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# Metadati utente {#user-metadata}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Endpoint API REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descrizione {#description}

Recupera i metadati condivisi da MVPD sull&#39;utente autenticato.

<div>


| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/token/usermetadata | App in streaming</br></br>o</br></br>Servizio programmatore | 1. richiedente</br>2.  deviceId (obbligatorio)</br>3.  device_info/X-Device-Info (obbligatorio)</br>4.  deviceType</br>5.  deviceUser (obsoleto)</br>6.  appId (obsoleto) | GET | XML o JSON contenente metadati utente o dettagli di errore in caso di errore. | 200 - Successo</br></br>404 - Nessun metadati trovato</br></br>412 - Token AuthN non valido (ad esempio, token scaduto) |


| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| device_info/</br></br>X-Device-Info | Informazioni sul dispositivo in streaming.</br></br>**Nota**: QUESTO PUÒ essere passato a device_info come parametro URL, ma a causa della dimensione potenziale di questo parametro e delle limitazioni della lunghezza di un URL GET, DEVE essere passato come X-Device-Info nell&#39;intestazione http. </br></br>Vedi tutti i dettagli in **Trasferimento delle informazioni sul dispositivo e sulla connessione** <!--http://tve.helpdocsonline.com/passing-device-information-->. |
| _deviceType_ | Tipo di dispositivo (ad esempio Roku, PC).</br></br>Se questo parametro è impostato correttamente, ESM offre metriche che [suddivisi per tipo di dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#progr-filter-metrics) quando utilizzi Clientless, in modo che sia possibile eseguire diversi tipi di analisi per esempio Roku, AppleTV, Xbox ecc.</br></br>Vedi [Vantaggi dell&#39;utilizzo del parametro del tipo di dispositivo senza client nelle metriche Pass ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Nota:** La `device_info` sostituisce questo parametro. </br> |
| _deviceUser_ | Identificatore utente del dispositivo.</br></br>**Nota:**se utilizzato, `deviceUser` deve avere gli stessi valori di nel [Crea codice di registrazione](/help/authentication/registration-code-request.md) richiesta. |
| _appId_ | ID/nome dell&#39;applicazione. </br></br>**Nota:**il `device_info` sostituisce questo parametro. Se utilizzato, `appId` deve avere gli stessi valori di nel **Crea codice di registrazione** richiesta. |

>[!NOTE]
> 
>Le informazioni sui metadati utente dovrebbero essere disponibili al termine del flusso di autenticazione, ma possono essere aggiornate sul flusso di autorizzazione, a seconda dell&#39;MVPD e del tipo di metadati.

</br>

## Risposta di esempio {#sample-response}

Dopo una chiamata riuscita, il server risponderà con un oggetto XML (predefinito) o JSON con una struttura simile a quella presentata di seguito:

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
              zip: ["12345", "34567"],
              maxRating: { 
                  "MPAA": "PG-13",
                  "VCHIP": "TV-Y", 
                  "URL": "http://exam.pl/e/manage/ratings"
              },
              householdID: "3456",
              userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
              channelID: ["channel-1", "channel-2"]
    }
```

Nella directory principale dell’oggetto sono presenti tre nodi:

* **aggiornato**: specifica una marca temporale UNIX che rappresenta l&#39;ultima volta che i metadati sono stati aggiornati. Questa proprietà verrà impostata inizialmente dal server durante la generazione dei metadati durante la fase di autenticazione. Le chiamate successive (dopo l’aggiornamento dei metadati) genereranno una marca temporale incrementata.

* **dati**: contiene i valori metadati effettivi.

* **cifrato**: array in cui sono elencate le proprietà crittografate. Per decrittografare un valore di metadati specifico, il programmatore deve eseguire una decodifica Base64 sui metadati, quindi applicare una decrittografia RSA sul valore risultante, utilizzando la propria chiave privata (ad Adobe crittografa i metadati sul server utilizzando il certificato pubblico del programmatore).

In caso di errore, il server restituirà un oggetto XML o JSON che specifica un messaggio di errore dettagliato.

Per ulteriori informazioni, consulta [Metadati utente](/help/authentication/user-metadata.md).

### [Torna a Riferimento API REST](/help/authentication/rest-api-reference.md).
