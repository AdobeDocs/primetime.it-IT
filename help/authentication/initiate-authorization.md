---
title: Avvia autorizzazione
description: Avvia autorizzazione
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Avvia autorizzazione {#initiate-authorization}

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

Ottiene la risposta dell&#39;autorizzazione. 

| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/autorizzare | App in streaming</br></br>o</br></br>Servizio programmatore | 1. richiedente (obbligatorio)</br>2.  deviceId (obbligatorio)</br>3.  risorsa (obbligatoria)</br>4.  device_info/X-Device-Info (obbligatorio)</br>5.  _deviceType_</br> 6.  _deviceUser_ (Obsoleto)</br>7.  _appId_ (Obsoleto)</br>8.  parametri aggiuntivi (facoltativo) | GET | XML o JSON contenente dettagli di autorizzazione o dettagli di errore in caso di errore. Di seguito sono riportati alcuni esempi. | 200 - Successo  </br>403 - Nessun successo |

{style=&quot;table-layout:auto&quot;}

</br>


| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| risorsa | Una stringa che contiene un resourceId (o frammento MRSS), identifica il contenuto richiesto da un utente ed è riconosciuta dagli endpoint di autorizzazione MVPD. |
| device_info/</br></br>X-Device-Info | Informazioni sul dispositivo in streaming.</br></br>**Nota**: QUESTO PUÒ essere passato a device_info come parametro URL, ma a causa della dimensione potenziale di questo parametro e delle limitazioni della lunghezza di un URL GET, DEVE essere passato come X-Device-Info nell&#39;intestazione http. </br></br>Vedi tutti i dettagli in [Trasferimento delle informazioni sul dispositivo e sulla connessione](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | Tipo di dispositivo (ad esempio Roku, PC).</br></br>Se questo parametro è impostato correttamente, ESM offre metriche che [suddivisi per tipo di dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) quando utilizzi Clientless, in modo che sia possibile eseguire diversi tipi di analisi per esempio Roku, AppleTV, Xbox ecc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**Nota**: il parametro device_info sostituirà questo parametro. |
| _deviceUser_ | Identificatore utente del dispositivo. |
| _appId_ | ID/nome dell&#39;applicazione. </br></br>**Nota**: device_info sostituisce questo parametro. |
| parametri aggiuntivi | La chiamata può anche contenere parametri facoltativi che abilitano altre funzionalità come:</br></br>* generic_data - consente l&#39;utilizzo di [TempPass promozionale](https://tve.helpdocsonline.com/promotional-temp-pass)</br></br>Esempio: `generic_data=("email":"email@domain.com")` |

{style=&quot;table-layout:auto&quot;}

>[!CAUTION]
>
>**Indirizzo IP del dispositivo di streaming**</br>
>Per le implementazioni da client a server, l&#39;indirizzo IP del dispositivo di streaming viene inviato in modo implicito con questa chiamata.  Per le implementazioni server-to-server, dove **regcode** La chiamata viene effettuata dal Servizio programmatori e non dal Dispositivo streaming, per trasmettere l&#39;indirizzo IP del dispositivo streaming è necessaria la seguente intestazione:</br></br>
>
>
```
>X-Forwarded-For : <streaming\_device\_ip>
>```
>
>dove `<streaming\_device\_ip>` è l&#39;indirizzo IP pubblico del dispositivo di streaming.</br></br>
>Esempio :</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1
>X-Forwarded-For:203.45.101.20
>```


### Risposta di esempio {#sample-response}

* **Caso 1: Completato**

</br>
  * **XML:**
  </br>
    ```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
    <expires>1348148289000</expires>
    <mvpd>sampleMvpdId</mvpd>
    <requestor>sampleRequestorId</requestor>
    <resource>sampleResourceId</resource>
    </authorization>
    ```



* **JSON:**

   ```JSON
   {
     "mvpd": "sampleMvpdId",
     "resource": "sampleResourceId",
     "requestor": "sampleRequestorId",
     "expires": "1348148289000"
   }
   ```

>[!IMPORTANT]
>
>Quando la risposta proviene da un proxy MVPD, può includere un elemento aggiuntivo denominato `proxyMvpd`. 

 

* **Caso 2: Autorizzazione negata**


   ```JSON
   <error>
     <status>403</status>
     <message>User not authorized</message>
     <details>Your subscription package does not include the "ASFAFD" channel.
     Please go to http://www.ca.ble/upgrade in order to upgrade your subscription.</details>
   </error>
   ```

[Torna a Riferimento API REST](http://tve.helpdocsonline.com/rest-api-reference)
