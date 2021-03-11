---
description: L'applicazione deve utilizzare gli oggetti PTTimedMetadata appropriati nei momenti opportuni.
title: Archiviare gli oggetti metadati temporizzati durante l'invio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# Archiviare gli oggetti metadati temporizzati durante l&#39;invio {#store-timed-metadata-objects-as-they-are-dispatched}

L&#39;applicazione deve utilizzare gli oggetti PTTimedMetadata appropriati nei momenti opportuni.

Durante l’analisi del contenuto, che avviene prima della riproduzione, TVSDK identifica i tag sottoscritti e notifica all’applicazione tali tag. Il tempo associato a ciascun `PTTimedMetadata` è il tempo assoluto sulla timeline della riproduzione.

L&#39;applicazione deve completare le seguenti attività:

1. Tenere traccia del tempo di riproduzione corrente.
1. Associa il tempo di riproduzione corrente agli oggetti `PTTimedMetadata` inviati.

1. Utilizzare il valore `PTTimedMetadata` in cui l&#39;ora di inizio è uguale al tempo di riproduzione corrente.

   >[!NOTE]
   >
   >Il codice seguente presuppone che ci sia una sola istanza `PTTimedMetadata` alla volta. Se sono presenti più istanze, l&#39;applicazione deve salvarle in modo appropriato in un dizionario. Un metodo consiste nel creare un array in un dato momento e memorizzare tutte le istanze in tale array.

   L&#39;esempio seguente mostra come salvare gli oggetti `PTTimedMetadata` in un `NSMutableDictionary (timedMetadataCollection)` con chiave in base all&#39;ora di inizio di ogni `timedMetadata`.

   ```
   NSMutableDictionary *timedMetadataCollection; 
   
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       if (!timedMetadataCollection) 
       { 
           timedMetadataCollection = [[NSMutableDictionary alloc] init]; 
       } 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey] retain]; 
       if ([timedMetadata.name  isEqualToString: @"#EXT-OATCLS-SCTE35"]) 
       { 
            NSLog(@"Adding timedMetadata %@ to timedMetadataCollection with time                      
                    %f",timedMetadata.name,CMTimeGetSeconds(timedMetadata.time)); 
   
           NSNumber *timedMetadataStartTime = [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
       [timedMetadata release]; 
   }
   ```

## Analisi dei tag Nielsen ID3 {#example_3B51E9D4AF2449FAA8E804206F873ECF}

Per estrarre il tag ID3 da analizzare, utilizza quanto segue sul metodo `onMediaPlayerSubscribedTagIdentified` :

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

Dopo aver analizzato il tag ID3, estrae i metadati specifici di Nielsen utilizzando quanto segue:

```
    (NSString *)parseNielsenUrlFromID3Tag:(NSString *)str 
    { 
    /* ID3 tag <AVMetadataItem: 0x15e58e60, identifier=id3/PRIV, keySpace=org.id3, key class = __NSCFString, key=PRIV, commonKey=(null), extendedLanguageTag=(null), dataType=(null), time= {110265598/4410000 = 25.004} 
 
    , duration= 
    {INVALID} 
 
    , startDate=(null), extras= 
    { info = "www.nielsen.com/X100zdCIGeIlgZnkYj6UvQ==/pI-X5FFk07770SXf2ZbI6g==/CE0C6​1TsDo0jIrNn9N2yTPe6nVG3dHZHfgS52fJeQjf9fJCga9tj4OW4NXPZ9fI1mx0gfYUPBXnjqolHemZPtn_FCoNg​8Dqw8-Auruf15fU04pJfXTTN0IgZ4iWBmeRiPpS9X100zdCIGeIlgZnkYj6UvVjmPIdY5jyRQTA=/00000/21778/00"; } 
 
    , value length=1> 
    */ 
 
NSString *nielsenStr = nil; 
for (NSString *keyValuePairString in [str componentsSeparatedByString:@", "]) 
{ 
if([keyValuePairString rangeOfString:@"nielsen.com"].location != NSNotFound) 
{ // Nielsen NSRange start = [keyValuePairString rangeOfString:@"\""]; NSRange end = [keyValuePairString rangeOfString:@"\";"]; nielsenStr = [keyValuePairString substringWithRange:NSMakeRange(start.location + 1, end.location-start.location)]; } 
 
} 
return nielsenStr; 
}
```
