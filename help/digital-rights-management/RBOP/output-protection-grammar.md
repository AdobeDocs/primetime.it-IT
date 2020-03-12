---
description: Questa sezione descrive la grammatica dell'input di configurazione, enfatizzando le opzioni di input valide e non valide e spiegando come vengono interpretati i campi facoltativi omessi.
seo-description: Questa sezione descrive la grammatica dell'input di configurazione, enfatizzando le opzioni di input valide e non valide e spiegando come vengono interpretati i campi facoltativi omessi.
seo-title: Grammatica RBOP
title: Grammatica RBOP
uuid: d9064e39-593a-4767-b835-287640b4c94a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Grammatica RBOP {#rbop-grammar}

Questa sezione descrive la grammatica dell&#39;input di configurazione, enfatizzando le opzioni di input valide e non valide e spiegando come vengono interpretati i campi facoltativi omessi.

La grammatica di protezione dell&#39;output basata sulla risoluzione è definita come una sequenza di regole, in cui ogni regola può avere più moduli validi:

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## Applicazione delle regole grammaticali {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>Per migliorare la leggibilità della grammatica, le seguenti proprietà non vengono riportate nella grammatica ma rimangono invariate:

1. L&#39;ordine delle coppie definite all&#39;interno degli oggetti non è fisso; quindi, ogni permutazione delle coppie è valida.

   Ad esempio, se abbiamo definito un oggetto come questo:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   quindi anche la seguente struttura è considerata valida: =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. Per ogni coppia all&#39;interno di un oggetto, si presume che solo 1 istanza di tale coppia esista all&#39;interno di una determinata istanza di un dato oggetto.

   Ad esempio, se abbiamo definito un oggetto come questo:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   l&#39;istanza seguente non è valida, perché all&#39;interno dello stesso oggetto sono presenti due `foo` coppie:

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   Allo stesso modo, con due oggetti quali:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   e:

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   è valido, in quanto sono istanze indipendenti dello stesso oggetto.

1. Per le definizioni in cui è possibile scegliere una o più sequenze di stringhe, trattare le stringhe come un insieme, in cui le voci duplicate vengono trattate come una singola voce. Ad esempio, `["foo", "bar", "foo", "baz"]` è equivalente a `["foo", "bar", "baz"]`

1. Per la definizione dei numeri, viene utilizzato uno spazio tra le regole (ad esempio, `Digit Digits`), ma non deve essere utilizzato tale spazio quando si applica la regola.

   Ad esempio, se esprimiamo il numero *123* per la regola NonZeroInteger, dovrebbe essere espresso come `123` anziché `1 2 3`, anche se la regola contiene uno spazio tra NonZeroDigit e Cifre.

1. Alcune delle regole consentono più moduli. In questi casi, i diversi moduli sono separati dal `'|'` carattere.

   Ad esempio, questa regola:

   ```
   Foo ::= "A" | "B" | "C"
   ```

   significa che un&#39;istanza di `Foo` può essere sostituita con &quot;A&quot;, &quot;B&quot; o &quot;C&quot;. Ciò non deve essere confuso con un modulo che si espande su più righe; si tratta di una funzione che consente di rendere più leggibili i moduli più lunghi.

## La grammatica {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

```
PixelBasedOPConfig ::= 
      {} 
    | { "maxPixel": NonNegativeInteger } 
    | { "pixelConstraints": PixelConstraintsSeq } 
    | { "pixelConstraints": PixelConstraintsSeq, 
        "maxPixel": NonNegativeInteger } 
 
PixelConstraintsSeq ::= 
      [] 
    | [ PixelConstraints ] 
 
PixelConstraints ::= 
      PixelConstraint 
    | PixelConstraint, PixelConstraints 
 
PixelConstraint ::= 
      { "pixelCount": NonNegativeInteger } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
         "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
 
DigitalOutputRestrictionsSeq ::= 
      [] 
    | [ DigitalOutputRestrictions ] 
 
DigitalRestrictions ::= 
      DigitalRestriction 
    | DigitalRestriction, DigitalRestrictions 
 
DigitalRestriction ::= 
      { "output": DigitalOutputOption } 
    | { "output": DigitalOutputOption, "hdcp": HDCP } 
 
DigitalOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "REQUIRED" 
    | "NO_PLAYBACK" 
 
HDCP ::= 
    { "major": PositiveInteger, "minor": NonNegativeInteger } 
 
AnalogOutputRestriction ::= 
    { "output": AnalogOutputOption } 
 
AnalogOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "USE_IF_AVAILABLE_ACP" 
    | "USE_IF_AVAILABLE_CGMSA" 
    | "REQUIRED" 
    | "REQUIRED_ACP" 
    | "REQUIRED_CGMSA" 
    | "NO_PLAYBACK" 
 
OTAOutputRestriction ::= 
    { "whitelist": OTAWhitelistSeq } 
 
OTAWhitelistSeq ::= 
      [] 
    | [ OTAWhitelist ] 
 
OTAWhitelist ::= 
      OTAConnectionType 
    | OTAConnectionType, OTAWhitelist 
 
OTAConnectionType ::= 
      "MIRACAST" 
    | "AIRPLAY" 
    | "WIDI" 
    | "DLNA" 
 
NonNegativeInteger ::= 
      Digit 
    | NonZeroDigit Digits 
 
PositiveInteger ::= 
      NonZeroDigit 
    | NonZeroDigit Digits 
 
Digits ::= 
      Digit 
    | Digit Digits 
 
Digit ::= 
      0 
    | NonZeroDigit

NonZeroDigit ::= 
      1 
    | 2 
    | 3 
    | 4 
    | 5 
    | 6 
    | 7 
    | 8 
    | 9
```

## Semantica: Configurazioni legali ma non valide {#section_709BE240FF0041D4A1B0A0A7544E4966}

L&#39;argomento Configurazione *protezione output di* esempio presentava una configurazione valida con il relativo significato semantico. La sezione precedente in *questo* argomento presentava le regole grammaticali per le configurazioni. Mentre la grammatica aiuta a garantire la correttezza sintattica, ci sono configurazioni sintattiche legali che non sono semanticamente corrette (cioè, non sono logiche). Questa sezione presenta configurazioni *sintatticamente* legali, ma *semanticamente* errate. Tenere presente che gli esempi di questa sezione sono stati ridotti alla struttura minima necessaria per illustrare lo scenario in discussione.

* Non è possibile definire più vincoli di pixel con lo stesso numero di pixel.

   ```
   {  
     "pixelConstraints":  
       [  
         { "pixelCount": 720 }  
       ]  
    }  
   ```

* Il conteggio dei pixel non deve superare la risoluzione massima in pixel specificata.

   ```
   { 
     "maxPixel": 720, 
     "pixelConstraints": 
       [ 
         {"pixelCount": 1080} 
       ] 
   } 
   ```
