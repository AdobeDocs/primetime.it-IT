---
description: L’implementazione di riferimento di Primetime utilizza un formato di feed basato su JSON per le risposte. Questo formato viene analizzato utilizzando un'implementazione dell'interfaccia IFeedItemAdapter.
title: Formato catalogo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Formato catalogo {#catalog-format}

L’implementazione di riferimento di Primetime utilizza un formato di feed basato su JSON per le risposte. Questo formato viene analizzato utilizzando un&#39;implementazione dell&#39;interfaccia IFeedItemAdapter.

>[!NOTE]
>
>Questo formato di feed è il formato di esempio utilizzato dall’implementazione di riferimento e serve come esempio di come il formato può essere analizzato e mappato all’interfaccia di feed. Puoi utilizzare il tuo formato di feed di input con le tue implementazioni di interfaccia di feed.

Ad alto livello, il formato è costituito da un array di voci di contenuto. Ogni voce rappresenta un contenuto video live o VOD pubblicato:

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

Ogni voce di feed è un oggetto JSON con un determinato set di attributi:

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
| `id` | Identificatore/guida univoco per il contenuto, in base a quanto impostato dal sistema di pubblicazione dei feed. |
| `title` | Titolo del contenuto. |
| `description` | Una descrizione del contenuto. |
| `categories` | Un elenco di categorie con tag per il contenuto che può essere utilizzato dall’applicazione per migliorare l’esperienza dell’utente. Leggi le proprietà del contenuto. |
| `keywords` | Un elenco di parole chiave separate da virgola può essere utilizzato dall’applicazione per migliorare l’esperienza dell’utente. Leggi le proprietà del contenuto. |
| `isLive` | true o false, che indica se si tratta di un flusso Live o VOD. |
| `content` | Array di oggetti JSON con formati alternativi per il contenuto e gli URL corrispondenti. Ad esempio, potrebbero esserci URL per i formati f4m e m3u8. Gli attributi dell’oggetto JSON sono descritti di seguito. |
| `thumbnails` | Array di oggetti JSON con URL per miniature di diverse dimensioni. Gli attributi dell’oggetto JSON sono definiti di seguito. |
| `metadata` | Oggetto JSON che definisce i metadati per il contenuto. Al momento questi metadati sono limitati ai metadati correlati all’annuncio. L’oggetto metadati è definito di seguito. |

Il seguente blocco di codice definisce gli oggetti JSON che formano l’array di **oggetti contenuto**:

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
| formato | Deve essere nel formato m3u8 per Android. |
| url | L’URL del flusso video per il formato specificato. |

Il seguente blocco di codice definisce gli oggetti JSON che formano l’array di **oggetti miniatura**:

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
| formato | Stringa che indica il formato del file miniatura, ad esempio JPEG, PNG, ecc. |
| altezza | Altezza della miniatura. Nell&#39;applicazione di riferimento, la miniatura con l&#39;altezza e la larghezza più piccole viene restituita come miniatura piccola e quella con larghezza e altezza maggiori come miniatura grande. |
| larghezza | Larghezza della miniatura. Nell&#39;applicazione di riferimento, la miniatura con l&#39;altezza e la larghezza più piccole viene restituita come miniatura piccola e quella con larghezza e altezza maggiori come miniatura grande. |
| url | URL del file miniature. |

Il seguente blocco di codice definisce **oggetto metadati**:

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
| annuncio | Metadati relativi all’annuncio. |
| tipo | Il valore può essere Annunci Primetime, Interruzioni pubblicitarie dirette o Marcatori annuncio personalizzati. <br/><br/>Il PSDK fornisce il supporto integrato per i seguenti tipi di metadati: metadati relativi all’Auditude per Primetime Ad Server (annunci Primetime), interruzioni pubblicitarie dirette con URL di annunci (interruzioni pubblicitarie dirette) e marcatori pubblicitari personalizzati che forniscono l’intervallo di tempo per ciascun marcatore pubblicitario (marcatori pubblicitari personalizzati). Ogni tipo dispone di un AdProvider integrato nel PSDK che elabora i metadati.  <br/><br/>Il formato JSON per ciascuno di questi è stato definito di seguito. |
| dettagli | Include gli attributi dei metadati dell’annuncio. Entrambi i tipi di metadati di annunci dispongono di un proprio set di attributi definito di seguito. Per i tipi incorporati, gli attributi inclusi definiscono i dati previsti dal PSDK per quel tipo. |
| adesione | Metadati relativi all’adesione |
| id | ID risorsa multimediale utilizzato per le richieste di autorizzazione per il servizio pass Adobe Primetime per TV a pagamento. L’ID può essere una stringa di testo o una stringa mRSS con codifica HTML. Qualsiasi contenuto multimediale che richiede l’autorizzazione deve contenere un ID risorsa valido. |
