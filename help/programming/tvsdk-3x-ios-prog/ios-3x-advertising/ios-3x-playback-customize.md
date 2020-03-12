---
description: Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.
seo-description: Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.
seo-title: Personalizzare la riproduzione con gli annunci
title: Personalizzare la riproduzione con gli annunci
uuid: b21a2b1b-5376-41cb-a772-a8945fd56f3c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Personalizzare la riproduzione con gli annunci {#customize-playback-with-ads}

Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.

>[!TIP]
>
>È possibile ignorare il comportamento predefinito utilizzando la `PTAdPolicySelector` classe.

Il comportamento predefinito varia a seconda che l&#39;utente superi o meno l&#39;interruzione dell&#39;annuncio durante la riproduzione normale o ricercando in un video.

Potete personalizzare il comportamento di riproduzione e riproduzione nei seguenti modi:

* Salvate la posizione in cui l’utente ha smesso di guardare il video e ha ripreso la riproduzione nella stessa posizione in una sessione futura.
* Se un&#39;interruzione di annuncio viene presentata all&#39;utente, non vengono visualizzati annunci aggiuntivi per un certo numero di minuti, anche se l&#39;utente cerca di trovare una nuova posizione.
* Se il contenuto non viene riprodotto dopo alcuni minuti, riavviate il flusso o eseguite il failover su un&#39;altra origine per lo stesso contenuto.

   Nella sessione di riproduzione del failover, per consentire all&#39;utente di saltare gli annunci e riprendere la posizione precedente, è possibile disattivare gli annunci pre-roll e/o mid-roll. TVSDK fornisce metodi per abilitare la disattivazione degli annunci pre-roll e mid-roll.

## Elementi API per la riproduzione di annunci {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK fornisce classi e metodi che possono essere utilizzati per personalizzare il comportamento di riproduzione del contenuto che contiene annunci pubblicitari.
I seguenti elementi API sono utili per personalizzare la riproduzione:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Elemento API</b></th> 
   <th colname="col2" class="entry"><b>Contenuto che supporta la pubblicità</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> Controllate se un'interruzione annuncio deve essere contrassegnata come osservata da un visualizzatore e, in caso affermativo, quando contrassegnarla. Impostate e ottenete il criterio controllato utilizzando la <span class="codeph"> proprietà </span> adBreakAsWatched. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> Protocollo che consente la personalizzazione del comportamento degli annunci TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Classe che implementa il comportamento TVSDK predefinito. L'applicazione può ignorare questa classe per personalizzare i comportamenti predefiniti senza implementare l'interfaccia completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>Ora locale della riproduzione, ad eccezione delle interruzioni pubblicitarie inserite. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> searchToLocalTime </span> . <p>In questo caso, la ricerca si verifica in relazione a un'ora locale nel flusso. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>La posizione virtuale sulla timeline viene convertita nella posizione locale. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched, </span> proprietà. Indica se il visualizzatore ha guardato l’annuncio. </td> 
  </tr> 
 </tbody> 
</table>

## Configurare la riproduzione personalizzata {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Prima di poter personalizzare o ignorare i comportamenti degli annunci, registra l’istanza dei criteri degli annunci con TVSDK.

Per personalizzare i comportamenti degli annunci, effettuate una delle seguenti operazioni:

* Conformarsi al `PTAdPolicySelector` protocollo e implementare tutti i metodi di selezione dei criteri richiesti.

   Questa opzione è consigliata se avete la necessità di ignorare **tutti** i comportamenti di annunci predefiniti.

* Escludete la `PTDefaultAdPolicySelector` classe e fornite implementazioni solo per quei comportamenti che richiedono la personalizzazione.

   Questa opzione è consigliata se dovete ignorare solo **alcuni** comportamenti predefiniti.

Per entrambe le opzioni, completare le seguenti attività:

1. Registra l’istanza del criterio che deve essere utilizzata da TVSDK tramite client factory.

   >[!NOTE]
   >
   >I criteri di annunci personalizzati registrati all&#39;inizio della riproduzione vengono cancellati quando l&#39; `PTMediaPlayer` istanza viene deallocata. L&#39;applicazione deve registrare un&#39;istanza del selettore criteri ogni volta che viene creata una nuova sessione di riproduzione.

   Ad esempio:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementa le personalizzazioni.

## Ignora interruzioni annuncio per un periodo di tempo {#section_99809BE4D9BB4DEEBBF596C746CA428A}

Per impostazione predefinita, TVSDK forza la riproduzione di un&#39;interruzione di annuncio quando l&#39;utente cerca su un&#39;interruzione di annuncio. Potete personalizzare il comportamento per saltare un&#39;interruzione annuncio se il tempo trascorso da un completamento interruzione precedente è compreso entro un certo numero di minuti.

>[!IMPORTANT]
>
>Quando viene eseguito un tentativo interno di saltare un annuncio, potrebbe verificarsi una leggera pausa nella riproduzione.

L&#39;esempio seguente di un selettore di criteri di pubblicità personalizzato salta gli annunci nei prossimi cinque minuti (ora dell&#39;orologio a muro) dopo che un utente ha visto un&#39;interruzione di annuncio.

1. Registra l’istanza del criterio che deve essere utilizzata da TVSDK tramite client factory.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementate la personalizzazione.

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

## Salvate la posizione del video e riprendete più tardi {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

Potete salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.

Gli annunci inseriti dinamicamente differiscono tra le sessioni utente, pertanto il salvataggio della posizione **con** gli annunci a giunzione fa riferimento a una posizione diversa in una sessione futura. TVSDK fornisce metodi per recuperare la posizione di riproduzione ignorando gli annunci in sequenza.

1. Quando l’utente esce da un video, l’applicazione recupera e salva la posizione nel video.

   >[!TIP]
   >
   >Le durate degli annunci non sono incluse.

   Le interruzioni di annuncio possono variare in ogni sessione a causa di pattern di annunci, limiti di frequenza e così via. L’ora corrente del video in una sessione potrebbe essere diversa in una sessione futura. Quando si salva una posizione nel video, l&#39;applicazione recupera l&#39;ora locale . Utilizzare la `localTime` proprietà per leggere questa posizione, che è possibile salvare sul dispositivo o in un database sul server.

   Ad esempio, se l’utente si trova al 20° minuto del video e questa posizione include cinque minuti di annunci, `currentTime` sarà di 1200 secondi, mentre `localTime` a questa posizione saranno 900 secondi.

   >[!IMPORTANT]
   >
   >L&#39;ora locale e l&#39;ora corrente sono uguali per i flussi live/lineari. In questo caso, `convertToLocalTime` non ha effetto. Per VOD, l&#39;ora locale rimane invariata mentre gli annunci suonano.

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

1. Per riprendere il video nella stessa posizione in cui era stato salvato dalla sessione precedente, utilizzate `seekToLocalTime`.

   >[!TIP]
   >
   >Questo metodo viene chiamato solo con valori di ora locali. Se il metodo viene chiamato con i risultati dell&#39;ora corrente, si verifica un comportamento non corretto.

   Per cercare l&#39;ora corrente, utilizza `seekToTime`.

1. Quando l&#39;applicazione riceve l&#39;evento `PTMediaPlayerStatusReady` di modifica dello stato, cerca l&#39;ora locale salvata.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Specifica le interruzioni di annuncio come specificato nell&#39;interfaccia dei criteri di annuncio.
1. Implementa un selettore di criteri di annunci personalizzato estendendo il selettore di criteri di annunci predefinito.
1. Fornire le interruzioni pubblicitarie che devono essere presentate all&#39;utente mediante l&#39;implementazione `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Questo metodo include un&#39;interruzione annuncio pre-roll e le interruzioni annuncio mid-roll prima della posizione dell&#39;ora locale. L&#39;applicazione può decidere di riprodurre un&#39;interruzione di annuncio pre-roll e riprendere fino all&#39;ora locale specificata, di riprodurre un&#39;interruzione di annuncio mid-roll e riprendere fino all&#39;ora locale specificata, o di non riprodurre interruzioni di annuncio.