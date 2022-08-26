---
title: Avvia autenticazione
description: Avvia autenticazione
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Avvia autenticazione {#initiate-authentication}

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

Avvia il processo di autenticazione informando di un evento di selezione MVPD. Crea un record nel database di autenticazione Primetime, riconciliato quando viene ricevuta una risposta corretta dall&#39;MVPD. 



| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate | Modulo AuthN | 1. requestor_id (obbligatorio)</br>2.  mso_id (obbligatorio)</br>3.  reg_code (obbligatorio)</br>4.  nome_dominio (obbligatorio)</br>5.  noflash=true -  </br>    (Obbligatorio, parametro residuo)</br>6.  no_iframe=true (obbligatorio, parametro residuo)</br>7.  parametri aggiuntivi (facoltativo)</br>8.  redirect_url (obbligatorio) | GET | L&#39;app Web di accesso viene reindirizzata alla pagina di accesso MVPD. | 302 per le implementazioni di reindirizzamento complete |

{style=&quot;table-layout:auto&quot;}


| Parametro di input | Descrizione |
| --- | --- |
| requestor_id | Richiedente programmatore per il quale l&#39;operazione è valida. |
| mso_id | ID MVPD per il quale l&#39;operazione è valida. |
| reg_code | Codice di registrazione generato dal servizio Reggie. |
| nome_dominio | Dominio di origine. |
| redirect_url | L’url di reindirizzamento dell’app Web di accesso dopo il completamento dell’autenticazione. |

{style=&quot;table-layout:auto&quot;}

</br>

>[!IMPORTANT]
> 
>**Importante: Parametri obbligatori -** Indipendentemente dall’implementazione lato client, tutti i parametri di cui sopra sono obbligatori.
>
>
>Esempio:    
>
>
```
>domain_name=loginwebapp.com
>mso_id=sampleMvpdId
>reg_code=RO0885W
>requestor_id=sampleRequestorId
>noflash=true
>redirect_url=http://loginwebapp.com
>```

>[!IMPORTANT]
> 
>**Importante: Parametri opzionali**
>
>La chiamata può anche contenere parametri facoltativi che abilitano altre funzionalità come:
>
> * generico\_data - consente l&#39;utilizzo di [TempPass promozionale](https://tve.helpdocsonline.com/promotional-temp-pass)
>
>```JSON
>Example:
>   generic_data=("email":"email@domain.com")
>```


### **Note** {#notes}

* Il valore del `domain_name` deve essere impostato su uno dei nomi di dominio registrati con l&#39;autenticazione Primetime. Per ulteriori informazioni, consulta [Registrazione e inizializzazione](http://tve.helpdocsonline.com/new-programmer-overview$reg_and_init).

* [Evita di usare &#39;&amp;&#39;reg\_code nella richiesta /authenticate (Nota tecnica)](https://tve.helpdocsonline.com/clientless:-avoid-using-&#39;&amp;&#39;reg_code-in-/authenticate-request)

* La `redirect_url` Il parametro deve essere l&#39;ultimo nell&#39;ordine

* Il valore del `redirect_url` Il parametro deve essere codificato in URL

[Torna a Riferimento API REST](http://tve.helpdocsonline.com/rest-api-reference)
