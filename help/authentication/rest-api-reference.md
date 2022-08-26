---
title: Riferimento API REST
description: Riferimento api residuo
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 3%

---


# Riferimento API REST {#rest-api-reference}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Formati di risposta {#response-formats}


>[!NOTE]
>
> Le API fornite in questi servizi possono restituire le risposte in XML o JSON (per le API che restituiscono una risposta). Nella richiesta sono disponibili 3 modi diversi per specificare il formato della risposta:
>* Imposta HTTP Accept Header su &quot;application/xml&quot;</code>&quot; o &quot;application/json</code>&quot;
>* Nel payload della richiesta, specifica il parametro &quot;format=xml</code>&quot; o &quot;format=json</code>&quot;</li>
>* Chiama l&#39;endpoint del servizio Web con estensione .xml</code> o .json</code>. Ad esempio, &quot;/regcode.xml</code>&quot; o &quot;/regcode.json</code>&quot;
>
>È possibile specificare uno qualsiasi dei metodi di cui sopra. Se si specificano più metodi con formati in conflitto, potrebbero verificarsi errori o output indesiderati.

## Endpoint API REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Riepilogo servizi Web {#web_srvs_summary}

La tabella seguente elenca i servizi web disponibili per l’approccio senza client. Fai clic sugli endpoint dei servizi web per ulteriori informazioni (richiesta e risposta di esempio, parametri di input, metodi HTTP, ecc.)


| Sr | Endpoint servizio Web | Descrizione | [Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration). | Ospitato a | Chiamata da |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode](http://tve.helpdocsonline.com/registration-code-request) | Restituisce il codice di registrazione generato in modo casuale e l’URI della pagina di login | 2 | Adobe  </br>Servizio Reg Code | Dispositivo avanzato |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/return-registration-record) | Restituisce il record del codice di registrazione contenente il codice di registrazione UUID, il codice di registrazione e l&#39;ID dispositivo con hash | 8 | Adobe  </br>Servizio Reg Code | Autenticazione Primetime |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](http://tve.helpdocsonline.com/provide-mvpd-list) | Restituisce l&#39;elenco degli MVPD configurati per il richiedente | 5 | Adobe  </br>Primetime  </br>autenticazione  </br>Servizio | Login  </br>Web  </br>App |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](http://tve.helpdocsonline.com/initiate-authentication) | Avvia il processo AuthN informando l&#39;evento di selezione MVPD. Crea un record sul database di autenticazione, riconciliato quando viene ricevuta una risposta corretta da MVPD (passaggio 13) | 7 | Adobe  </br>Primetime  </br>autenticazione  </br>Servizio | Login  </br>Web  </br>App |
| 5. | Consumatore dell&#39;asserzione SAML | Flusso di lavoro SAML esistente tra l&#39;autenticazione Primetime e MVPD | 13 | Primetime  </br>autenticazione  </br>Servizio | Autenticazione Primetime |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](http://tve.helpdocsonline.com/check-authentication-flow-by-second-screen-web-app) | L&#39;app Web di accesso può verificare se il flusso di accesso tentato è stato eseguito correttamente |  | Primetime  </br>autenticazione   </br>Servizio | Login   </br>Web   </br>App |
| 7. | [&lt;sp_fqdn>/api/v1/token/autenticazione](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | Ottiene i metadati correlati al token AuthN | 15 | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/delete-registration-record) | Elimina il record del codice reg e rilascia il codice reg da riutilizzare | 16 | Adobe  </br>Servizio Reg Code | Autenticazione Primetime |
| 9. | [&lt;sp_fqdn>/api/v1/autorizzare](http://tve.helpdocsonline.com/initiate-authorization) | Ottiene la risposta dell&#39;autorizzazione. | 17 | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](http://tve.helpdocsonline.com/check-authentication-token) | Indica se il dispositivo dispone di un token AuthN non scaduto. |  | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |
| 11. | [&lt;sp_fqdn>/api/v1/token/autenticazione](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | Restituisce il token AuthN se trovato. |  | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |
| 12. | [&lt;sp_fqdn>/api/v1/token/authz](http://tve.helpdocsonline.com/retrieve-authorization-token) | Restituisce il token AuthZ se trovato. |  | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |
| 13. | [&lt;sp_fqdn>/api/v1/token/media](http://tve.helpdocsonline.com/obtain-short-media-token) | Restituisce il token per contenuti multimediali brevi se trovato - come /api/v1/mediatoken |  | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](http://tve.helpdocsonline.com/obtain-short-media-token) | Ottiene il token per contenuti multimediali brevi |  | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |
| 15. | [&lt;sp_fqdn>/api/v1/preautorizzare](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources) | Recupera l’elenco delle risorse preautorizzate |  | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |
| 16. | [&lt;sp_fqdn>/api/v1/preautorizzare/{code}](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources-by-way-of-web-app) | Recupera l’elenco delle risorse preautorizzate |  | Primetime  </br>autenticazione  </br>Servizio | App Web di accesso |
| 17. | [&lt;sp_fqdn>/api/v1/logout](http://tve.helpdocsonline.com/logout) | Rimuovere i token AuthN e AuthZ dallo storage |  | Primetime  </br>autenticazione   </br>Servizio | Dispositivo avanzato |
| 18. | [&lt;sp_fqdn>/api/v1/token/usermetadata](http://tve.helpdocsonline.com/user-metadata-call) | Ottiene i metadati utente al termine del flusso di autenticazione | N/D | N/D | Dispositivo avanzato |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](http://tve.helpdocsonline.com/free-preview-for-temp-pass-and-promotional-temp-pass) | Crea un token di autenticazione per Temp Pass o Promozionale Temp Pass | N/D | Primetime  </br>autenticazione  </br>Servizio | Dispositivo avanzato |

{style=&quot;table-layout:auto&quot;}

## Sicurezza API REST {#security}

Tutte le API senza client di autenticazione Primetime devono essere chiamate utilizzando il protocollo HTTPS per una comunicazione sicura. Inoltre, la maggior parte delle API chiamate deve contenere un token di accesso fornito da [Registrazione client dinamica](http://tve.helpdocsonline.com/dynamic-client-registration).


## Informazioni correlate {#related}

* [Panoramica API REST](http://tve.helpdocsonline.com/reset-api-overview)
* [Guida di riferimento server-to-server](http://tve.helpdocsonline.com/server-to-server-cookbook)
* [Cartella di lavoro Client-to-Server](http://tve.helpdocsonline.com/client-to-server)
* [Evita di usare &#39;&amp;&#39;reg\_code nella richiesta /authenticate (Nota tecnica)](https://tve.zendesk.com/entries/23648011-Clientless-Avoid-using-reg-code-in-authenticate-request)
