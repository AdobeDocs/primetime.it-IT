---
description: La richiesta e la risposta di adesione vengono trasmesse tramite una connessione SSL reciprocamente autenticata tra il server licenze e il servizio di adesione del cliente.
seo-description: La richiesta e la risposta di adesione vengono trasmesse tramite una connessione SSL reciprocamente autenticata tra il server licenze e il servizio di adesione del cliente.
seo-title: API SEES Public
title: API SEES Public
uuid: f3a17d61-04ee-4bdb-9d64-a98066c6d1c8
translation-type: tm+mt
source-git-commit: 15403abbd53486e1faa2146cda83f41bd8116632

---


# API SEES Public {#sees-public-api}

La richiesta e la risposta di adesione vengono trasmesse tramite una connessione SSL reciprocamente autenticata tra il server licenze e il servizio di adesione del cliente.

Lo schema URI HTTPS ( [https://tools.ietf.org/html/rfc7230#section-2.7.2](https://tools.ietf.org/html/rfc7230#section-2.7.2)) viene utilizzato per definire l&#39;endpoint di adesione e per la richiesta viene utilizzato il metodo di richiesta HTTP POST ( [https://tools.ietf.org/html/rfc7231#section-4.3.3](https://tools.ietf.org/html/rfc7231#section-4.3.3)). L&#39;endpoint di adesione, così come un flag che indica l&#39;adesione back-end, è obbligatorio e deve essere incluso nel criterio al momento della creazione del pacchetto.

## Richiesta di adesione {#section_BFBFEF0795CA46D6842C479256B95F95}

Il corpo della richiesta di adesione sarà un oggetto JSON definito come mostrato di seguito.

**Definizione dell&#39;oggetto di richiesta di adesione JSON**

```
{ 
 "title" : "Entitlement Request", 
 "type" : "object", 
 "properties" : { 
  "messageID" : { 
   "type" : "string", 
   "description" : "Unique ID for this message (GUID).  Used to confirm that the subsequent response is actually for this request." 
  }, 
  "version" : { 
   "type" : "integer", 
   "description" : "Version number of the protocol, currently 1." 
  }, 
  "requestType" : { 
   "type" : "integer", 
   "description" : "Request type. 1 - time based entitlement request, 2 - device registration entitlement request 3 - device bound entitlement request." 
  }, 
  "contentID" : { 
   "type" : "string", 
   "description" : "Content ID (GUID) that was given to the content during packaging time." 
  }, 
  "customerCookie" : { 
   "type" : "string", 
   "description" : "Customer cookie. Cookie is just arbitrary string up to 32 characters long." 
  } 
    }, 
 "required" : ["messageID", "version", "contentID"] 
}
```

## Risposta di adesione {#section_F15A9FD6BAD946B3B4C5C14612F90154}

Il corpo della risposta di adesione è un oggetto JSON.

**Definizione dell&#39;oggetto di risposta per l&#39;adesione JSON**

```
{ 
  "title" : "Entitlement Response", 
  "type" : "object", 
  "properties" : { 
    "messageID" : { 
    "type" : "string", 
    "description" : "Unique ID from the Entitlement Request message.   
      Must match, or entitlement will be denied." 
  }, 
  "version" : { 
    "type" : "integer", 
    "description" : "Version number of the protocol; must be <= the version number  
      from the Entitlement Request message." 
  }, 
  "isAllowed" : { 
    "type" : "boolean", 
    "description" : "Grant the license or not." 
  }, 
  "epTokenURL" : { 
    "type" : "string", 
    "description" : "ExpressPlay Token URL" 
  }, 
  "error" : { 
    "type" : "integer", 
    "description" : "An error number produced by the entitlement server.  
      Will be passed to the client as the 'code' field of the server error response." 
  }, 
  "errorText" : { 
    "type" : "string", 
    "description" : "Additional error information produced by the entitlement server.  
      Will be passed to the client as the 'text' field of the server error response." 
  }, 
  "required" : ["messageID", "version", "isAllowed", "epTokenURL"] 
}
```
