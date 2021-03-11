---
description: Questa sezione descrive la grammatica dell’input di configurazione, enfatizzando le opzioni di input valide e non valide e spiegando come vengono interpretati i campi facoltativi omessi.
title: Grammatica RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---


# Grammatica RBOP {#rbop-grammar}

Questa sezione descrive la grammatica dell’input di configurazione, enfatizzando le opzioni di input valide e non valide e spiegando come vengono interpretati i campi facoltativi omessi.

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
>Per migliorare la leggibilità della grammatica, le seguenti proprietà non vengono riportate nella grammatica ma rimangono vere:

1. L’ordine delle coppie definite all’interno degli oggetti non è fisso; pertanto, qualsiasi permutazione delle coppie è valida.

   Ad esempio, se abbiamo definito un oggetto come questo:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   allora anche la seguente struttura sarebbe considerata valida: =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. Per ogni coppia all&#39;interno di un oggetto, si presume che esista solo 1 istanza di tale coppia all&#39;interno di una determinata istanza di un dato oggetto.

   Ad esempio, se abbiamo definito un oggetto come questo:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   l&#39;istanza seguente non è valida, perché all&#39;interno dello stesso oggetto sono presenti due coppie `foo`:

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   Allo stesso modo, avendo due oggetti come:

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

1. Per le definizioni in cui è possibile scegliere una o più sequenze di stringhe, trattare le stringhe come un set, in cui le voci duplicate vengono trattate come una singola voce. Ad esempio, `["foo", "bar", "foo", "baz"]` equivale a `["foo", "bar", "baz"]`

1. Per la definizione dei numeri, viene utilizzato uno spazio tra le regole (ad esempio, `Digit Digits`), ma non deve essere utilizzato uno spazio simile durante l’applicazione della regola.

   Ad esempio, se esprimiamo il numero *cento ventitré* per la regola NonZeroInteger, deve essere espresso come `123` anziché come `1 2 3`, anche se la regola contiene uno spazio tra NonZeroDigit e Cifre.

1. Alcune delle regole consentono più moduli. In questi casi, i diversi moduli sono separati dal carattere `'|'`.

   Ad esempio, questa regola:

   ```
   Foo ::= "A" | "B" | "C"
   ```

   significa che un&#39;istanza di `Foo` può essere sostituita con &quot;A&quot;, &quot;B&quot; o &quot;C&quot;. Non confonderlo con un modulo che si estende su più righe; questa è una funzione per rendere i moduli più lunghi più leggibili.

## Grammatica {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

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

L&#39;argomento *Configurazione della protezione dell&#39;output di esempio* presenta una configurazione valida con il relativo significato semantico. La sezione precedente in *questo* argomento presentava le regole grammaticali per le configurazioni. Mentre la grammatica aiuta a garantire la correttezza sintattica, ci sono configurazioni legali sintatticamente che non sono semanticamente corrette (cioè, non sono logiche). Questa sezione presenta configurazioni *sintatticamente* legali, ma *semanticamente* non corrette. Tenere presente che gli esempi contenuti in questa sezione sono stati ridotti alla struttura minima necessaria per illustrare lo scenario in discussione.

* Non è possibile definire più vincoli di pixel con lo stesso conteggio di pixel.

   ```
   {  
     "pixelConstraints":  
       [  
         { "pixelCount": 720 }  
       ]  
    }  
   ```

* Il conteggio dei pixel non deve superare la risoluzione massima dei pixel specificata.

   ```
   { 
     "maxPixel": 720, 
     "pixelConstraints": 
       [ 
         {"pixelCount": 1080} 
       ] 
   } 
   ```
