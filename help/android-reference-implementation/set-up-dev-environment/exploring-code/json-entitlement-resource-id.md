---
title: Oggetto JSON per ID risorsa adesione
description: Il seguente blocco di codice fornisce un esempio di oggetto JSON quando l'ID della risorsa di adesione è una stringa di testo semplice.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Oggetto JSON per ID risorsa adesione {#json-object-for-entitlement-resource-id}

Il seguente blocco di codice fornisce un esempio di oggetto JSON quando l&#39;ID della risorsa di adesione è una stringa di testo semplice. In questo caso, l’ID risorsa è la stringa &quot;resource&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

Il seguente blocco di codice fornisce un esempio di oggetto JSON quando l&#39;ID della risorsa di adesione è una stringa mRSS con codifica HTML.

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
