---
title: Verifica token di autenticazione
description: Verifica token di autenticazione
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Verifica token di autenticazione {#check-authentication-token}

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

Indica se il dispositivo dispone di un token di autenticazione non scaduto.

| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/checkauthn | App in streaming</br></br>o</br></br>Servizio programmatore | 1. richiedente (obbligatorio)</br>2.  deviceId (obbligatorio)</br>3.  device_info/X-Device-Info (obbligatorio)</br>4.  _deviceType_ </br>5.  _deviceUser_ (Obsoleto)</br>6.  _appId_ (Obsoleto) | GET | XML o JSON contenente i dettagli dell’errore in caso di errore. | 200 - Successo   </br>403 - Nessun successo |

{style=&quot;table-layout:auto&quot;}


| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| device_info/</br></br>X-Device-Info | Informazioni sul dispositivo in streaming.</br></br>**Nota**: QUESTO PUÒ essere passato a device_info come parametro URL, ma a causa della dimensione potenziale di questo parametro e delle limitazioni della lunghezza di un URL GET, DEVE essere passato come X-Device-Info nell&#39;intestazione http. </br></br>Vedi tutti i dettagli in [Trasferimento delle informazioni sul dispositivo e sulla connessione](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | Tipo di dispositivo (ad esempio Roku, PC).</br></br>Se questo parametro è impostato correttamente, ESM offre metriche che [suddivisi per tipo di dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) quando utilizzi Clientless, in modo che sia possibile eseguire diversi tipi di analisi per esempio Roku, AppleTV, Xbox ecc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**Nota**: il parametro device_info sostituirà questo parametro. |
| _deviceUser_ | Identificatore utente del dispositivo. |
| _appId_ | ID/nome dell&#39;applicazione.</br>**Nota**: device_info sostituisce questo parametro. |

{style=&quot;table-layout:auto&quot;}


## Risposta (in caso di esito negativo) {#response}

```JSON
    <error>
      <status>403</status>
      <message>Authentication token expired</message>
    </error>
```

### [Torna a Riferimento API REST](http://tve.helpdocsonline.com/rest-api-reference)
