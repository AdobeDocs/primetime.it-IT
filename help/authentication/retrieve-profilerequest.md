---
title: Recupera richiesta profilo SSO piattaforma
description: Recupera richiesta profilo SSO piattaforma
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Recupera richiesta profilo SSO piattaforma {#retrieve-platform-sso-profile-request}

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

Questa risorsa genera richieste di profilo per un requestor ID e una tupla MVPD.


| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{requestor}/profile-requests/{mvpd} | App in streaming</br></br>o</br></br>Servizio programmatore | 1. requestor (parametro di percorso)</br>2. mvpd (parametro del percorso)</br>3. deviceType (obbligatorio) | GET | La risposta Content-Type sarà application/octet-stream, in quanto il payload effettivo è opaco per l&#39;applicazione client.</br></br>La risposta deve essere inoltrata dall’applicazione alla piattaforma</br></br>Motore SSO per ottenere un SSO profilo. | 200 - Successo   </br>400 - Richiesta errata |


| Parametro di input | Descrizione |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| mvpd | ID MVPD per il quale l&#39;operazione è valida. |
| deviceType | Piattaforma Apple per la quale stiamo tentando di ottenere una richiesta di profilo.  O **iOS** o **tvOS**. |

### [Torna a Riferimento API REST](http://tve.helpdocsonline.com/rest-api-reference)
