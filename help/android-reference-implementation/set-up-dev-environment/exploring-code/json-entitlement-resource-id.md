---
seo-title: Oggetto JSON per ID risorsa di adesione
title: Oggetto JSON per ID risorsa di adesione
uuid: f5b659da-1732-404c-bf00-d32a0ae39aa1
description: Il seguente blocco di codice fornisce un esempio di oggetto JSON quando l'ID risorsa di adesione è una semplice stringa di testo.
seo-description: Il seguente blocco di codice fornisce un esempio di oggetto JSON quando l'ID risorsa di adesione è una semplice stringa di testo.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Oggetto JSON per ID risorsa di adesione {#json-object-for-entitlement-resource-id}

Il seguente blocco di codice fornisce un esempio di oggetto JSON quando l&#39;ID risorsa di adesione è una semplice stringa di testo. In questo caso, l&#39;ID risorsa è la stringa &quot;resource&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

Il seguente blocco di codice fornisce un esempio di oggetto JSON quando l&#39;ID risorsa di adesione è una stringa mRSS con codifica HTML.

```
<rss version="2.0" xmlns:media="https://search.yahoo.com/mrss/"> 
<channel> 
<title>REF_ADOBE</title> 
<item> 
<title>Adobe Primetime Reference</title> 
<guid>1234</guid> 
<media:rating scheme="urn:v-chip">TV-PG</media:rating> 
</item> 
</channel> 
</rss>
```

La seguente stringa mRSS viene utilizzata come ID risorsa.

```
"metadata" : { 
    "entitlement" : { 
        "id" : "<rss version=&quot;2.0&quot; 
        xmlns:media=&quot; 
        https://search.yahoo.com/mrss/&quot; 
        ><channel><title>REF_ADOBE</title><item> 
        <title>Adobe Primetime Reference</title><guid> 
        1234</guid><media:rating scheme=&quot;urn:v-chip&quot;> 
        TV-PG</media:rating></item></channel></rss>" 
        } 
} 
```
