---
description: Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.
seo-description: Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.
seo-title: Implementazione di un risolutore di contenuti personalizzato
title: Implementazione di un risolutore di contenuti personalizzato
uuid: 88627fdc-3b68-4a9f-847e-a490ea8e3034
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---


# Implementazione di un risolutore di contenuto personalizzato {#implement-a-custom-content-resolver}

Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.

Quando TVSDK rileva una nuova opportunità, esegue un&#39;iterazione attraverso i risolutori di contenuti registrati alla ricerca di una in grado di risolvere tale opportunità. Il primo che restituisce true è selezionato per la risoluzione dell&#39;opportunità. Se non è in grado di risolvere il problema, tale opportunità viene ignorata. Poiché il processo di risoluzione del contenuto è in genere asincrono, il risolutore del contenuto è responsabile della notifica del completamento del processo.

1. Create un&#39;istanza `AdvertisingFactory` personalizzata ed eseguite l&#39;override di `createContentResolver`.

   Ad esempio:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public ContentResolver createContentResolver(MediaPlayerItem item) { 
           Metadata metadata = _mediaPlayer.getCurrentItem().getResource().getMetadata(); 
           if (metadata != null) { 
               if (metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue())) { 
                   return new AuditudeResolver(getActivity().getApplicationContext()); 
               } else if (metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY.getValue())) { 
                   return new MetadataResolver(); 
               } else if (metadata.containsKey(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue())) { 
                   return new CustomAdMarkersContentResolver(); 
               } else if (metadata.containsKey(CustomAdResolver.CUSTOM_METADATA_KEY)) { 
                   return new CustomAdResolver(); 
               } 
           } 
           return null; 
       } 
       ... 
   }
   ```

1. Registra il produttore del client di annunci in `MediaPlayer`.

   Ad esempio:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Trasmettere un oggetto `AdvertisingMetadata` a TVSDK nel modo seguente:
   1. Creare un oggetto `AdvertisingMetadata` e un oggetto `MetadataNode`.
   1. Salvare l&#39;oggetto `AdvertisingMetadata` in `MetadataNode`.

   ```java
   MetadataNode result = new MetadataNode(); 
   result.setNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue(),  
                  advertisingMetadata);
   ```

1. Create una classe ad resolver personalizzata che estenda la classe `ContentResolver`.
   1. Nel risolutore annunci personalizzato, ignora questa funzione protetta:

      ```java
      void doResolveAds(Metadata metadata,  
                        PlacementOpportunity placementOpportunity)
      ```

      I metadati contengono il `AdvertisingMetada`. Utilizzatelo per la generazione di vettore `TimelineOperation` seguente.

   1. Per ogni opportunità di posizionamento, create un `Vector<TimelineOperation>`.

      Il vettore può essere vuoto, ma non nullo.

      Questo esempio `TimelineOperation` fornisce una struttura per `AdBreakPlacement`:

      ```java
      AdBreakPlacement(AdBreak.createAdBreak( 
                                ads,       // Vector<Ad> 
                                time,      // Ad Break start time. Note: local time on the timeline 
                                duration,  // Ad Break duration 
                                tag()      // An arbitrary string value that can be attached to  
                                           // the AdBreak object. 
                               ), placementInformation  // Retrieved from PlacementOpportunity 
      )
      ```

   1. Dopo la risoluzione degli annunci, chiama una delle seguenti funzioni:

      * Se la risoluzione dell&#39;annuncio ha esito positivo: `notifyResolveComplete(Vector<TimelineOperation> proposals)`
      * Se la risoluzione dell&#39;annuncio non riesce: `notifyResolveError(Error error)`

      Ad esempio, se non riesce:

      ```java
      Metadata metadata = new MetadataNode(); 
      metadata.setValue("NATIVE_ERROR_CODE", exception.getCause().toString()); 
      error.setMetadata(metadata);
      ```


<!--<a id="example_4F0D7692A92E480A835D6FDBEDBE75E7"></a>-->

Questo esempio di risolutore di annunci personalizzato effettua una richiesta HTTP al server di annunci e riceve una risposta JSON.

```java
public class CustomAdResolver extends ContentResolver { 
    ... 
    @Override 
    protected void doResolveAds(Metadata metadata, PlacementOpportunity placementOpportunity) { 
        ... 
        if (resolveSuccess == true) { 
            notifyResolveComplete(Vector<TimelineOperation> proposals); 
        } 
        else { 
            notifyResolveError(Error error); 
        } 
    } 
    ... 
}
```

Esempio di risposta JSON e server per un flusso live:

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } 
        ] }, 
        { 
            "start": -1, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 
```

Esempio di risposta JSON e server per VOD:

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": {  
                } 
            }, 
            { 
                "id": 1002, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/crescent/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset2", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 50000, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 100000000, 
            "ads": [ { 
                "id": 1004, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/camry/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset4", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 
```

