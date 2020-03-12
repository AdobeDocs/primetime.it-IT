---
description: Per le risposte, l'implementazione di riferimento di Primetime utilizza un formato di feed basato su JSON. Questo formato viene analizzato utilizzando un'implementazione dell'interfaccia IFeedItemAdapter.
seo-description: Per le risposte, l'implementazione di riferimento di Primetime utilizza un formato di feed basato su JSON. Questo formato viene analizzato utilizzando un'implementazione dell'interfaccia IFeedItemAdapter.
seo-title: Formato catalogo
title: Formato catalogo
uuid: 6e1a526f-c0bb-403d-a792-666caf5479a5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Formato catalogo {#catalog-format}

Per le risposte, l&#39;implementazione di riferimento di Primetime utilizza un formato di feed basato su JSON. Questo formato viene analizzato utilizzando un&#39;implementazione dell&#39;interfaccia IFeedItemAdapter.

>[!NOTE]
>
>Questo formato di feed è il formato di esempio utilizzato dall&#39;implementazione di riferimento e serve da esempio per analizzare e mappare il formato all&#39;interfaccia del feed. Puoi usare il tuo formato di feed di input con le tue implementazioni di interfaccia di feed.

Ad alto livello, il formato è costituito da un array di voci di contenuto. Ogni voce rappresenta un contenuto video live o pubblicato con VOD:

```
{
    "entries": [
        {
        },
        {
        },
        ...
    ]
}
```

Ogni voce di feed è un oggetto JSON con un set specifico di attributi:

```
{
    "entries": [
        
            "id": "episode1",
            "title": "My episode1",
            "description": "This is an episode.",
            "categories": "documentary, educational, children",
            "keywords": "List, of, comma, separated, keywords",
            "isLive": false,
            "content":  [
                
                },
                
                },
            ],
            "thumbnails": [
                
                },
                
                }
            ]
            "metadata": 
            } 
        }
    ]
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | Un identificatore/guida univoco per il contenuto impostato dal sistema di pubblicazione dei feed. |
| `title` | Titolo per il contenuto. |
| `description` | Una descrizione del contenuto. |
| `categories` | Elenco di categorie con tag per il contenuto che può essere utilizzato dall&#39;applicazione per migliorare l&#39;esperienza dell&#39;utente. Leggere le proprietà per il contenuto. |
| `keywords` | L&#39;applicazione può utilizzare un elenco di parole chiave separate da virgola per migliorare l&#39;esperienza dell&#39;utente. Leggere le proprietà per il contenuto. |
| `isLive` | true o false, indicando se si tratta di un flusso Live o VOD. |
| `content` | Un array di oggetti JSON con formati alternativi per il contenuto e gli URL corrispondenti. Ad esempio, potrebbero essere presenti URL per i formati f4m e m3u8. Gli attributi dell&#39;oggetto JSON sono descritti di seguito. |
| `thumbnails` | Un array di oggetti JSON con URL per diverse dimensioni di miniature. Gli attributi dell&#39;oggetto JSON sono definiti di seguito. |
| `metadata` | Un oggetto JSON che definisce i metadati per il contenuto. Attualmente questi metadati sono limitati ai metadati correlati agli annunci. L&#39;oggetto metadata è definito di seguito. |

Il seguente blocco di codice definisce gli oggetti JSON che formano l&#39;array di oggetti **di** contenuto:

```
"content":  [
    {
        "format": "M3U8",
        "url": "https://adobeprimetime-f.akamaihd.net/i/
<i>longstringofcharacters</i>/
                 Episode_,640x360_1000,640x360_700,_b.mp4.csmil/master.m3u8",
        "language": "en"
    }  
],
```

| Proprietà | Descrizione |
|--- |--- |
| format | Deve essere in formato m3u8 per Android. |
| url | URL del flusso video per il formato specificato. |

Il seguente blocco di codice definisce gli oggetti JSON che formano l&#39;array di oggetti **** miniatura:

```
"thumbnails": [
    {
        "format": "JPEG",
        "height":  "90",
        "width": "160",
        "url": "https://example.com/small.jpg"
    },
    {
        "format": "JPEG",
        "height": "450",
        "width": "800",
        "url": "https://example.com/large.jpg"
    }
],
```

| Proprietà | Descrizione |
|---|---|
| format | Una stringa che indica il formato del file della miniatura, ad esempio JPEG, PNG, ecc. |
| height | Altezza della miniatura. Nell’applicazione di riferimento, la miniatura con altezza e larghezza più piccole viene restituita come miniatura piccola e quella con larghezza e altezza maggiori viene restituita come miniatura grande. |
| width | Larghezza della miniatura. Nell’applicazione di riferimento, la miniatura con altezza e larghezza più piccole viene restituita come miniatura piccola e quella con larghezza e altezza maggiori viene restituita come miniatura grande. |
| url | URL del file della miniatura. |

Il seguente blocco di codice definisce l&#39;oggetto **** metadata:

```
"metadata" : {
    "ad" : {
        "type" : "",
        "details" : {
        }
    }
    "entitlement" : {
        "id" : ""
    }
}
```

| Proprietà | Descrizione |
|--- |--- |
| ad | Metadati relativi agli annunci. |
| type | Il valore può essere Annunci Primetime, Interruzioni Annunci Dirette o Marcatori Annunci Personalizzati. <br/><br/>PSDK fornisce supporto integrato per i seguenti tipi di metadati: Metadati relativi all&#39;audience per Primetime Ad Serving (Primetime Ads), interruzioni pubblicitarie dirette con URL di annunci (Direct Ad Breaks) e marcatori di annunci personalizzati che forniscono l&#39;TimeRange per ciascun indicatore di annunci (Custom Ad Markers). Ciascun tipo dispone di un AdProvider integrato nel PSDK che elabora i metadati.  <br/><br/>Il formato JSON per ciascuno di questi è stato definito di seguito. |
| details | Include gli attributi dei metadati degli annunci. Entrambi i tipi di metadati di annunci dispongono di un proprio set di attributi definiti di seguito. Per i tipi incorporati, gli attributi inclusi definiscono i dati previsti dal PSDK per quel tipo. |
| entitlement | Metadati relativi all&#39;adesione |
| id | ID risorsa multimediale utilizzata per le richieste di autorizzazione per il servizio pass TV a pagamento di Adobe Primetime. L’ID può essere una stringa di testo o una stringa mRSS con codifica HTML. Qualsiasi contenuto multimediale che richiede l&#39;autorizzazione deve contenere un ID risorsa valido. |

