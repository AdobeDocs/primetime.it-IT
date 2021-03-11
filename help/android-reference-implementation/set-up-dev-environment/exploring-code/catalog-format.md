---
description: L’implementazione di riferimento di Primetime utilizza un formato di feed basato su JSON per le risposte. Questo formato viene analizzato utilizzando un'implementazione dell'interfaccia IFeedItemAdapter.
title: Formato catalogo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Formato del catalogo {#catalog-format}

L’implementazione di riferimento di Primetime utilizza un formato di feed basato su JSON per le risposte. Questo formato viene analizzato utilizzando un&#39;implementazione dell&#39;interfaccia IFeedItemAdapter.

>[!NOTE]
>
>Questo formato di feed è il formato di esempio utilizzato dall’implementazione di riferimento e funge da esempio di come il formato può essere analizzato e mappato all’interfaccia di feed. Puoi utilizzare il tuo formato di feed di input con le tue implementazioni di interfaccia di feed.

Ad alto livello, il formato è costituito da una matrice di voci di contenuto. Ogni voce rappresenta un contenuto video pubblicato in diretta o VOD:

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
| `id` | Identificatore/guida univoco per il contenuto impostato dal sistema di pubblicazione dei feed. |
| `title` | Un titolo per il contenuto. |
| `description` | Una descrizione del contenuto. |
| `categories` | Un elenco di categorie con tag per il contenuto che può essere utilizzato dall&#39;applicazione per migliorare l&#39;esperienza dell&#39;utente. Leggi le proprietà del contenuto. |
| `keywords` | L&#39;applicazione può utilizzare un elenco di parole chiave separate da virgola per migliorare l&#39;esperienza dell&#39;utente. Leggi le proprietà del contenuto. |
| `isLive` | true o false, che indica se si tratta di un flusso Live o VOD. |
| `content` | Matrice di oggetti JSON con formati alternativi per il contenuto e gli URL corrispondenti. Ad esempio, potrebbero esserci url per i formati f4m e m3u8. Gli attributi dell’oggetto JSON sono descritti più avanti di seguito. |
| `thumbnails` | Un array di oggetti JSON con url per dimensioni diverse di miniature. Gli attributi dell’oggetto JSON sono definiti di seguito. |
| `metadata` | Un oggetto JSON che definisce i metadati per il contenuto, attualmente questi sono limitati ai metadati correlati agli annunci. L&#39;oggetto metadati è definito di seguito. |

Il seguente blocco di codice definisce gli oggetti JSON che formano la matrice di **oggetti contenuto**:

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

Il seguente blocco di codice definisce gli oggetti JSON che formano la matrice di **oggetti miniatura**:

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
| format | Una stringa che indica il formato del file di miniatura, ad esempio JPEG, PNG, ecc. |
| altezza | Altezza della miniatura. Nell&#39;applicazione di riferimento, la miniatura con altezza e larghezza più piccole viene restituita come miniatura piccola e quella con larghezza e altezza maggiori viene restituita come miniatura grande. |
| larghezza | Larghezza della miniatura. Nell&#39;applicazione di riferimento, la miniatura con altezza e larghezza più piccole viene restituita come miniatura piccola e quella con larghezza e altezza maggiori viene restituita come miniatura grande. |
| url | URL del file di miniatura. |

Il seguente blocco di codice definisce l&#39; **oggetto metadati**:

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
| annuncio | Metadati relativi agli annunci. |
| type | Il valore può essere Annunci Primetime, Annunci diretti o Marcatori pubblicitari personalizzati. <br/><br/>Il PSDK fornisce supporto integrato per i seguenti tipi di metadati: Metadati relativi all’audience per Primetime Ad Serving (Primetime Ads), interruzioni pubblicitarie dirette con url degli annunci (Direct Ad Breaks) e marcatori pubblicitari personalizzati che forniscono l’Intervallo di tempo per ogni marcatore di annuncio (Custom Ad Markers). Ciascun tipo dispone di un AdProvider integrato nel PSDK che elabora i metadati.  <br/><br/>Di seguito è stato definito il formato JSON per ciascuno di questi. |
| dettagli | Include gli attributi dei metadati dell&#39;annuncio. Entrambi i tipi di metadati di annunci presentano un proprio set di attributi definiti di seguito. Per i tipi incorporati, gli attributi inclusi definiscono i dati previsti dal PSDK per quel tipo. |
| diritto | Metadati relativi all’autorizzazione |
| id | ID risorsa multimediale utilizzato per le richieste di autorizzazione per il servizio pass Adobe Primetime pay-TV. L&#39;ID può essere una stringa di testo o una stringa mRSS con codifica HTML. Qualsiasi contenuto multimediale che richiede l’autorizzazione deve contenere un ID risorsa valido. |

