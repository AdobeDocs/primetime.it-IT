---
title: Oggetto JSON per ID risorsa adesione
description: Il blocco di codice seguente fornisce un esempio di oggetto JSON quando l’ID della risorsa spettante è una stringa di testo semplice.
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Oggetto JSON per ID risorsa adesione {#json-object-for-entitlement-resource-id}

Il blocco di codice seguente fornisce un esempio di oggetto JSON quando l’ID della risorsa spettante è una stringa di testo semplice. In questo caso, l’ID risorsa è la stringa &quot;resource&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

Il blocco di codice seguente fornisce un esempio di oggetto JSON quando l’ID della risorsa spettante è una stringa mRSS con codifica HTML.

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

La seguente stringa mRSS viene utilizzata come ID di risorsa.

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
