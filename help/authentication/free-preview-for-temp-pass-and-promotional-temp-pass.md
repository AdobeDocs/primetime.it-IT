---
title: Anteprima gratuita per Temp Pass e Promozionale Temp Pass
description: Anteprima gratuita per Temp Pass e Promozionale Temp Pass
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---


# Anteprima gratuita per Temp Pass e Promozionale Temp Pass {#free-preview-for-temp-pass-and-promotional-temp-pass}

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

Consente la creazione di un token di autenticazione per Temp Pass e Promozionale Temp Pass senza la necessità di una seconda schermata.


| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate/freepreview | App in streaming</br></br>o</br></br>Servizio programmatore | 1. requestor_id (obbligatorio)</br>    </br>2.  deviceId (obbligatorio)</br>    </br>3.  mso_id (obbligatorio)</br>    </br>4.  nome_dominio (obbligatorio)</br>    </br>5.  device_info/X-Device-Info (obbligatorio)</br>6.  deviceType</br>    </br>7.  deviceUser (obsoleto)</br>    </br>8.  appId (obsoleto)</br>    </br>9.  generic_data (facoltativo) | POST | La risposta corretta sarà No Content (Nessun contenuto) 204, il che indica che il token è stato creato correttamente ed è pronto per l’uso per i flussi di autenticazione. | 204 - Nessun contenuto   </br>400 - Richiesta errata |

<div>


| Parametro di input | Descrizione |
| --- | --- |
| requestor_id | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| mso_id | ID MVPD per il quale l&#39;operazione è valida. |
| nome_dominio | Nome di dominio per il quale verrà concesso un token. Questo viene confrontato con i domini del provider di servizi quando viene concesso un token di autorizzazione. |
| device_info/</br></br>X-Device-Info | Informazioni sul dispositivo in streaming.</br></br>**Nota**: QUESTO PUÒ essere passato a device_info come parametro URL, ma a causa della dimensione potenziale di questo parametro e delle limitazioni della lunghezza di un URL GET, DEVE essere passato come X-Device-Info nell&#39;intestazione http. </br></br>Vedi tutti i dettagli in [Trasferimento delle informazioni sul dispositivo e sulla connessione](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | Tipo di dispositivo (ad esempio Roku, PC).</br></br>Se questo parametro è impostato correttamente, ESM offre metriche che [suddivisi per tipo di dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) quando utilizzi Clientless, in modo che sia possibile eseguire diversi tipi di analisi per esempio Roku, AppleTV, Xbox ecc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**Nota**: il parametro device_info sostituirà questo parametro. |
| _deviceUser_ | Identificatore utente del dispositivo.</br></br>**Nota**: se utilizzato, deviceUser deve avere gli stessi valori di nel [Crea codice di registrazione](http://tve.helpdocsonline.com/registration-code-request) richiesta. |
| _appId_ | ID/nome dell&#39;applicazione. </br></br>**Nota**: device_info sostituisce questo parametro. Se utilizzato, `appId` deve avere gli stessi valori di nel [Crea codice di registrazione](http://tve.helpdocsonline.com/create-registration-page-/-login-uri) richiesta. |
| generic_data | Utilizzato per limitare l’ambito del token per il passaggio temporaneo promozionale. |


### [Torna a Riferimento API REST](http://tve.helpdocsonline.com/rest-api-reference)
