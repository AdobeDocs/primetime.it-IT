---
description: Quando la riproduzione raggiunge un’interruzione pubblicitaria, passa un’interruzione pubblicitaria o termina in un’interruzione pubblicitaria, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento della testina di riproduzione corrente.
title: Personalizzare la riproduzione con gli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---

# Personalizzare la riproduzione con gli annunci {#customize-playback-with-ads}

Quando la riproduzione raggiunge un’interruzione pubblicitaria, passa un’interruzione pubblicitaria o termina in un’interruzione pubblicitaria, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento della testina di riproduzione corrente.

>[!TIP]
>
>È possibile ignorare il comportamento predefinito utilizzando `PTAdPolicySelector` classe.

Il comportamento predefinito varia a seconda che l’utente superi l’interruzione pubblicitaria durante la riproduzione normale o effettuando la ricerca in un video.

Puoi personalizzare il comportamento di riproduzione degli annunci nei seguenti modi:

* Salvare la posizione in cui l&#39;utente ha interrotto la visualizzazione del video e riprendere la riproduzione nella stessa posizione in una sessione futura.
* Se viene presentata all’utente un’interruzione pubblicitaria, non verranno mostrati annunci aggiuntivi per un numero di minuti, anche se l’utente cerca di trovare una nuova posizione.
* Se dopo alcuni minuti il contenuto non viene riprodotto correttamente, riavviare il flusso o eseguire il failover su un&#39;origine diversa per lo stesso contenuto.

  Nella sessione di riproduzione del failover, per consentire all’utente di saltare gli annunci e riprendere la precedente posizione di errore, puoi disabilitare gli annunci pre-roll e/o mid-roll. TVSDK fornisce metodi per consentire di saltare gli annunci pre-roll e mid-roll.

## Elementi API per la riproduzione di annunci {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK fornisce classi e metodi che è possibile utilizzare per personalizzare il comportamento di riproduzione dei contenuti che contengono annunci pubblicitari.
I seguenti elementi API sono utili per personalizzare la riproduzione:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Elemento API</b></th> 
   <th colname="col2" class="entry"><b>Contenuti che supportano la pubblicità</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> Controlla se un’interruzione pubblicitaria deve essere contrassegnata come se fosse stata guardata da un visualizzatore e, in caso affermativo, quando contrassegnarla. Imposta e ottieni la policy controllata utilizzando <span class="codeph"> adBreakAsWatched </span> proprietà. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> Protocollo che consente di personalizzare il comportamento degli annunci TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Classe che implementa il comportamento TVSDK predefinito. L’applicazione può eseguire l’override di questa classe per personalizzare i comportamenti predefiniti senza implementare l’interfaccia completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>Si tratta dell’ora locale della riproduzione, escluse le interruzioni pubblicitarie inserite. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> . <p>In questo caso, la ricerca si verifica in relazione a un’ora locale nel flusso. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>La posizione virtuale sulla timeline viene convertita nella posizione locale. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched </span> proprietà. Indica se il visualizzatore ha guardato l’annuncio. </td> 
  </tr> 
 </tbody> 
</table>

## Impostare la riproduzione personalizzata {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Prima di poter personalizzare o ignorare i comportamenti degli annunci, registra l’istanza dei criteri degli annunci con TVSDK.

Per personalizzare i comportamenti degli annunci, effettuare una delle seguenti operazioni:

* Conforme a `PTAdPolicySelector` e implementare tutti i metodi di selezione dei criteri richiesti.

  Questa opzione è consigliata se devi eseguire l’override di **tutto** i comportamenti di annuncio predefiniti.

* Ignora `PTDefaultAdPolicySelector` e forniscono implementazioni solo per i comportamenti che richiedono personalizzazione.

  Questa opzione è consigliata solo se è necessario eseguire l&#39;override **alcuni** dei comportamenti predefiniti.

Per entrambe le opzioni, completa le seguenti attività:

1. Registra l’istanza dei criteri che deve essere utilizzata da TVSDK tramite la client factory.

   >[!NOTE]
   >
   >I criteri di annuncio personalizzati registrati all’inizio della riproduzione vengono cancellati quando il `PTMediaPlayer` istanza deallocata. L’applicazione deve registrare un’istanza del selettore dei criteri ogni volta che viene creata una nuova sessione di riproduzione.

   Ad esempio:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementare le personalizzazioni.

## Ignorare le interruzioni pubblicitarie per un periodo di tempo {#section_99809BE4D9BB4DEEBBF596C746CA428A}

Per impostazione predefinita, TVSDK forza la riproduzione di un’interruzione pubblicitaria quando l’utente cerca sopra un’interruzione pubblicitaria. Puoi personalizzare il comportamento per saltare un’interruzione pubblicitaria se il tempo trascorso dal completamento di un’interruzione precedente è entro un determinato numero di minuti.

>[!IMPORTANT]
>
>Quando è presente una ricerca interna per saltare un annuncio, potrebbe essere presente una leggera pausa nella riproduzione.

L’esempio seguente di selettore di criteri di annuncio personalizzato ignora gli annunci nei successivi cinque minuti (tempo di clock a parete) dopo che un utente ha guardato un’interruzione pubblicitaria.

1. Registra l’istanza dei criteri che deve essere utilizzata da TVSDK tramite la client factory.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementa la personalizzazione.

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

## Salva la posizione del video e riprendi in un secondo momento {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

È possibile salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.

Gli annunci inseriti in modo dinamico differiscono tra le sessioni utente, pertanto la posizione viene salvata **con** gli annunci uniti si riferiscono a una posizione diversa in una sessione futura. TVSDK fornisce metodi per recuperare la posizione di riproduzione ignorando gli annunci uniti.

1. Quando l’utente chiude un video, l’applicazione recupera e salva la posizione all’interno del video.

   >[!TIP]
   >
   >Le durate degli annunci non sono incluse.

   Le interruzioni pubblicitarie possono variare in ogni sessione a causa di modelli di annunci, limiti di frequenza e così via. L’ora corrente del video in una sessione potrebbe essere diversa in una sessione futura. Quando si salva una posizione nel video, l’applicazione recupera l’ora locale. Utilizza il  `localTime` per leggere questa posizione , che puoi salvare sul dispositivo o in un database sul server.

   Ad esempio, se l’utente si trova al 20° minuto del video e questa posizione include cinque minuti di annunci, `currentTime` sarà di 1200 secondi, mentre `localTime` in questa posizione sarà di 900 secondi.

   >[!IMPORTANT]
   >
   >L’ora locale e l’ora corrente sono le stesse per i flussi live/lineari. In questo caso, `convertToLocalTime` non ha alcun effetto. Per VOD, l’ora locale rimane invariata durante la riproduzione degli annunci.

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

1. Per riprendere il video nella stessa posizione in cui era stato salvato nella sessione precedente, utilizza `seekToLocalTime`.

   >[!TIP]
   >
   >Questo metodo viene chiamato solo con valori di ora locali. Se il metodo viene chiamato con i risultati dell&#39;ora corrente, si verifica un comportamento errato.

   Per cercare fino all&#39;ora corrente, utilizzare `seekToTime`.

1. Quando l&#39;applicazione riceve `PTMediaPlayerStatusReady` evento di modifica dello stato, cerca nell’ora locale salvata.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Specifica le interruzioni pubblicitarie come specificato nell’interfaccia dei criteri relativi agli annunci.
1. Implementa un selettore di criteri per annunci personalizzato estendendo il selettore di criteri per annunci predefinito.
1. Fornisci le interruzioni pubblicitarie che devono essere presentate all&#39;utente implementando `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Questo metodo include un’interruzione pubblicitaria pre-roll e le interruzioni pubblicitarie mid-roll prima della posizione temporale locale. L’applicazione può decidere di riprodurre un’interruzione pubblicitaria pre-roll e riprendere all’ora locale specificata, riprodurre un’interruzione pubblicitaria mid-roll e riprendere all’ora locale specificata oppure non riprodurre interruzioni pubblicitarie.
