---
title: Avvia disconnessione
description: Avvia disconnessione
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Avvia disconnessione {#initiate-logout}

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

Rimuovere i token AuthN e AuthZ dallo storage.


| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/logout | App in streaming</br></br>o</br></br>Servizio programmatore | 1. richiedente</br>2.  deviceId (obbligatorio)</br>3.  device_info/X-Device-Info (obbligatorio)</br>4.  _deviceType_</br> 5.  _deviceUser_ (Obsoleto)</br>6.  _appId_ (Obsoleto) | DELETE | Nessuno | 204 |


| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| device_info/</br></br>X-Device-Info | Informazioni sul dispositivo in streaming.</br></br>**Nota**: QUESTO PUÒ essere passato a device_info come parametro URL, ma a causa della dimensione potenziale di questo parametro e delle limitazioni della lunghezza di un URL GET, DEVE essere passato come X-Device-Info nell&#39;intestazione http. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | Tipo di dispositivo (ad esempio Roku, PC).</br></br>Se questo parametro è impostato correttamente, ESM offre metriche che [suddivisi per tipo di dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) quando utilizzi Clientless, in modo che sia possibile eseguire diversi tipi di analisi per esempio Roku, AppleTV, Xbox ecc.</br></br>Vedi [Vantaggi dell&#39;utilizzo del parametro del tipo di dispositivo senza client nelle metriche di passaggio ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Nota**: il parametro device_info sostituirà questo parametro. |
| _deviceUser_ | Identificatore utente del dispositivo.</br></br>**Nota**: se utilizzato, deviceUser deve avere gli stessi valori di nel [Crea codice di registrazione](/help/authentication/registration-code-request.md) richiesta. |
| _appId_ | ID/nome dell&#39;applicazione. </br></br>**Nota**: device_info sostituisce questo parametro. Se utilizzato, `appId` deve avere gli stessi valori di nel [Crea codice di registrazione](/help/authentication/registration-code-request.md) richiesta. |

>[!IMPORTANT]
> 
>La chiamata di logout attualmente presenta la seguente limitazione: cancella i token AuthN e AuthZ dallo storage (cioè, sul lato programmatore / autenticazione Primetime), ma **non** chiama l&#39;endpoint di logout MVPD. 


