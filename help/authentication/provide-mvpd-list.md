---
title: Fornire l'elenco MVPD
description: Fornire l'elenco MVPD
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Fornire l&#39;elenco MVPD {#provide-mvpd-list}

## Endpoint API REST {#clientless-endpoints}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

&lt;reggie_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## Descrizione {#description}

Restituisce l&#39;elenco degli MVPD configurati per il richiedente.

| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/config/{requestorId}</br></br>Ad esempio:</br></br>&lt;sp_fqdn>/api/v1/config/sampleRequestorId | Autenticazione Primetime | 1. Richiedente</br>    (componente Percorso)</br>_2.  deviceType (obsoleto)_ | GET | XML o JSON contenente l’elenco degli MVPD. | 200 |

{style=&quot;table-layout:auto&quot;}


| Parametro di input | Descrizione |
| --------------- | ------------------------------------------------------------- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| *deviceType* | Tipo di dispositivo. |

{style=&quot;table-layout:auto&quot;}

### Risposta di esempio {#sample-response}

Come la risposta XML MVPD esistente al servlet /config

Nota: Tutti gli MVPD configurati per utilizzare Platform SSO avranno le seguenti proprietà extra all’interno del nodo corrispondente (JSON/XML):

* **enablePlatformServices (booleano):** flag che indica se questo MVPD è integrato tramite Platform SSO
* **boardingStatus (stringa):** flag che indica se l&#39;MVPD supporta completamente l&#39;SSO della piattaforma (SUPPORTED) o se l&#39;MVPD appare solo nel selettore della piattaforma (PICKER)
* **displayInPlatformPicker (booleano):** Questo MVPD dovrebbe comparire nel selettore della piattaforma
* **platformMappingId (stringa):** l’identificatore di questo MVPD noto dalla piattaforma
* **requiredMetadataFields (array stringa):** i campi di metadati utente dovrebbero essere disponibili in caso di accesso riuscito


[Torna a Clientless API Reference](http://tve.helpdocsonline.com/clientless-api-reference)
