---
description: Quando la riproduzione raggiunge un'interruzione pubblicitaria, passa un'interruzione pubblicitaria o termina in un'interruzione pubblicitaria, TVSDK definisce un comportamento predefinito per il posizionamento della testina di riproduzione corrente.
title: Personalizzare la riproduzione con gli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# Personalizza la riproduzione con gli annunci{#customize-playback-with-ads}

Quando la riproduzione raggiunge un&#39;interruzione pubblicitaria, passa un&#39;interruzione pubblicitaria o termina in un&#39;interruzione pubblicitaria, TVSDK definisce un comportamento predefinito per il posizionamento della testina di riproduzione corrente.

>[!TIP]
>
>È possibile ignorare il comportamento predefinito utilizzando la classe `PTAdPolicySelector` .

Il comportamento predefinito varia a seconda che l’utente passi l’interruzione pubblicitaria durante la riproduzione normale o la ricerca in un video.

Puoi personalizzare il comportamento della riproduzione di annunci nei seguenti modi:

* Salvare la posizione in cui l’utente ha interrotto la visualizzazione del video e riprendere la riproduzione nella stessa posizione in una sessione futura.
* Se all’utente viene presentata un’interruzione pubblicitaria, non vengono visualizzati annunci aggiuntivi per un numero di minuti, anche se l’utente cerca una nuova posizione.
* Se la riproduzione del contenuto non riesce dopo alcuni minuti, riavviare il flusso o eseguire il failover su un&#39;altra origine per lo stesso contenuto.

   Nella sessione di riproduzione del failover, per consentire all&#39;utente di saltare gli annunci e riprendere la precedente posizione di errore, è possibile disabilitare gli annunci pre-roll e/o mid-roll. TVSDK fornisce metodi per abilitare l’eliminazione degli annunci pre-roll e mid-roll.

## Elementi API per la riproduzione di annunci {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK fornisce classi e metodi che è possibile utilizzare per personalizzare il comportamento di riproduzione dei contenuti che contengono annunci pubblicitari.
I seguenti elementi API sono utili per personalizzare la riproduzione:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento API </th> 
   <th colname="col2" class="entry"> Contenuto che supporta la pubblicità </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata  </span> </td> 
   <td colname="col2"> Controlla se un'interruzione pubblicitaria deve essere contrassegnata come osservata da un visualizzatore e, in caso affermativo, quando contrassegnarla. Imposta e ottieni il criterio controllato utilizzando la proprietà <span class="codeph"> adBreakAsWatched </span> . </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector  </span> </td> 
   <td colname="col2"> Protocollo che consente la personalizzazione del comportamento degli annunci TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> Classe che implementa il comportamento TVSDK predefinito. L'applicazione può ignorare questa classe per personalizzare i comportamenti predefiniti senza implementare l'interfaccia completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer  </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localeTime  </span>. <p>Ora locale della riproduzione, escluse le interruzioni pubblicitarie inserite. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> cercaToLocalTime  </span> . <p>In questo caso, la ricerca si verifica in relazione a un’ora locale nel flusso. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime  </span>. <p>La posizione virtuale nella timeline viene convertita nella posizione locale. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak  </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched,  </span> proprietà. Indica se il visualizzatore ha guardato l’annuncio. </td> 
  </tr> 
 </tbody> 
</table>

## Imposta riproduzione personalizzata {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Prima di poter personalizzare o sovrascrivere i comportamenti degli annunci, registra l’istanza del criterio degli annunci con TVSDK.

Per personalizzare i comportamenti degli annunci, effettua una delle seguenti operazioni:

* Conformarsi al protocollo `PTAdPolicySelector` e implementare tutti i metodi di selezione dei criteri richiesti.

   Questa opzione è consigliata se devi sovrascrivere **all** i comportamenti di annunci predefiniti.

* Ignora la classe `PTDefaultAdPolicySelector` e fornisci implementazioni solo per quei comportamenti che richiedono personalizzazione.

   Questa opzione è consigliata se è necessario ignorare solo **alcuni** dei comportamenti predefiniti.

Per entrambe le opzioni, completa le attività seguenti:

1. Registra l&#39;istanza dei criteri che deve essere utilizzata da TVSDK attraverso il client factory.

   >[!NOTE]
   >
   >I criteri degli annunci personalizzati registrati all&#39;inizio della riproduzione vengono cancellati quando l&#39;istanza `PTMediaPlayer` viene deallocata. L&#39;applicazione deve registrare un&#39;istanza del selettore dei criteri ogni volta che viene creata una nuova sessione di riproduzione.

   Ad esempio:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementa le tue personalizzazioni.

## Ignora interruzioni pubblicitarie per un periodo di tempo {#section_99809BE4D9BB4DEEBBF596C746CA428A}

Per impostazione predefinita, TVSDK forza la riproduzione di un’interruzione pubblicitaria quando l’utente cerca tramite un’interruzione pubblicitaria. Puoi personalizzare il comportamento per saltare un’interruzione pubblicitaria se il tempo trascorso da un precedente completamento dell’interruzione si trova entro un certo numero di minuti.

>[!IMPORTANT]
>
>Quando si verifica una ricerca interna per saltare un annuncio, potrebbe verificarsi una leggera pausa nella riproduzione.

L&#39;esempio seguente di un selettore di criteri di annunci personalizzati salta gli annunci nei cinque minuti successivi (tempo di clock della bacheca) dopo che un utente ha guardato un&#39;interruzione di pubblicità.

1. Registra l&#39;istanza dei criteri che deve essere utilizzata da TVSDK attraverso il client factory.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementa la tua personalizzazione.

**PTS5MinuteSkipBreakPolicySelector.h**

```
#import "PTMediaPlayerNotifications.h" 
#import "PTMediaPlayer.h" 
#import "PTDefaultAdPolicySelector.h" 
 
//  extend the default policy  
selector@interface PTS5MinuteSkipBreakPolicySelector : PTDefaultAdPolicySelector 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player; 
  
@end
```

**PTS5MinuteSkipBreakPolicySelector.m**

```
#import "PTS5MinuteSkipBreakPolicySelector.h" 
  
double MIN_BREAK_INTERVAL  = 60 * 5; // 5 minutes 
  
@implementation PTS5MinuteSkipBreakPolicySelector 
{ 
    PTMediaPlayer *_player; 
    NSTimeInterval _lastAdBreakPlayedTime; 
} 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player 
{ 
    if (self = [super init]) 
    { 
        _lastAdBreakPlayedTime = 0; 
        _player = [player retain]; 
        [self addobservers]; 
    } 
    
    return self; 
} 
  
- (NSArray *)selectAdBreaksToPlay:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectAdBreaksToPlay (%f): %f", self,  
        CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectAdBreaksToPlay:info]; 
    } 
    
    return nil; 
} 
  
- (PTAdBreakPolicyType)selectPolicyForAdBreak:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectPolicyForAdBreak (%f): %f  %f", self,  
            CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime,  
            [[NSDate date] timeIntervalSince1970]); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectPolicyForAdBreak:info]; 
    } 
    
    return PTAdBreakPolicyTypeSkip; 
} 
  
- (BOOL)shouldPlayAdBreaks 
{ 
    NSTimeInterval currentTime = [[NSDate date] timeIntervalSince1970]; 
    if (_lastAdBreakPlayedTime <= 0) 
    { 
        return YES; 
    } 
    
    if (_lastAdBreakPlayedTime > 0 && (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) 
    { 
        return YES; 
    } 
    
    // don't play any ad break if 5 minutes hasn't elapsed 
    return NO; 
} 
  
- (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification 
{ 
    NSLog(@"%@ - AdBreak Start", self); 
} 
  
- (void) onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
{ 
    _lastAdBreakPlayedTime = [[NSDate date] timeIntervalSince1970]; 
    NSLog(@"%@ - AdBreak Complete at: %f", self, _lastAdBreakPlayedTime); 
} 
  
- (void)addobservers 
{ 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
                name:PTMediaPlayerAdBreakStartedNotification object:_player]; 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
                name:PTMediaPlayerAdBreakCompletedNotification object:_player]; 
} 
  
- (void)removeObservers 
{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
} 
  
- (void)dealloc 
{ 
    [self removeObservers]; 
    [_player release]; 
    [super dealloc]; 
} 
  
@end
```

## Salva la posizione del video e riprendi più tardi {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

È possibile salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.

Gli annunci inseriti in modo dinamico differiscono tra le sessioni utente, pertanto il salvataggio della posizione **con** annunci uniti fa riferimento a una posizione diversa in una sessione futura. TVSDK fornisce metodi per recuperare la posizione di riproduzione ignorando gli annunci in sequenza.

1. Quando l&#39;utente chiude un video, l&#39;applicazione recupera e salva la posizione nel video.

   >[!TIP]
   >
   >Le durate degli annunci non sono incluse.

   Le interruzioni di annunci possono variare in ogni sessione a causa di pattern di annunci, limiti di frequenza e così via. L&#39;ora corrente del video in una sessione potrebbe essere diversa in una sessione futura. Quando si salva una posizione nel video, l&#39;applicazione recupera l&#39;ora locale . Utilizza la proprietà `localTime` per leggere questa posizione , che puoi salvare sul dispositivo o in un database sul server.

   Ad esempio, se l’utente si trova al 20° minuto del video e questa posizione include cinque minuti di annunci, `currentTime` sarà di 1200 secondi, mentre `localTime` in questa posizione sarà di 900 secondi.

   >[!IMPORTANT]
   >
   >L&#39;ora locale e l&#39;ora attuale sono gli stessi per i flussi live/lineari. In questo caso, `convertToLocalTime` non ha alcun effetto. Per VOD, l&#39;ora locale rimane immutata mentre gli annunci suonano.

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
   
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double seekableRangeStart = CMTimeGetSeconds(seekableRange.start); 
           double seekableRangeDuration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentTime); // includes ads 
           double localTime = CMTimeGetSeconds(self.player.localTime); // no ads 
       } 
   }
   ```

1. Per riprendere il video nella stessa posizione: Per riprendere la riproduzione del video dalla posizione salvata da una sessione precedente, utilizza `seekToLocalTime`

   >[!TIP]
   >
   >Questo metodo viene chiamato solo con valori di ora locali. Se il metodo viene chiamato con i risultati dell&#39;ora corrente, si verifica un comportamento errato.

   Per cercare l&#39;ora corrente, utilizza `seekToTime`.

1. Quando l&#39;applicazione riceve l&#39;evento di modifica dello stato `PTMediaPlayerStatusReady`, cerca l&#39;ora locale salvata.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Fornisci le interruzioni pubblicitarie come specificato nell&#39;interfaccia dei criteri per gli annunci.
1. Implementa un selettore di criteri di annunci personalizzato estendendo il selettore di criteri di annunci predefinito.
1. Fornire le interruzioni pubblicitarie che devono essere presentate all&#39;utente implementando `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Questo metodo include un&#39;interruzione pubblicitaria pre-roll e le interruzioni pubblicitarie mid-roll prima della posizione dell&#39;ora locale. L&#39;applicazione può decidere di riprodurre un annuncio pre-roll e riprendere all&#39;ora locale specificata, riprodurre un&#39;interruzione pubblicitaria mid-roll e riprendere all&#39;ora locale specificata, o riprodurre senza interruzioni pubblicitarie.

