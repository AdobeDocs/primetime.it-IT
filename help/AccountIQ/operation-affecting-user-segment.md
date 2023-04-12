---
title: Crea un’operazione su un segmento utente e tiene traccia dell’effetto
description: Come creare un'operazione che effetti e tiene traccia dell'effetto su un segmento di utenti definito.
exl-id: ab74f857-e178-4120-8f9c-655ec921d096
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Creazione di un’operazione su un segmento utente {#operation-to-track-segment}

Ogni pagina di report sul QI dell&#39;account ha un **Crea nuova operazione** per facilitare la creazione di flussi di lavoro per automatizzare (e semplificare) varie azioni (in blocco) sugli account degli abbonati; definire regole per specificare un campione, definire azioni e registrare e analizzare gli effetti di tali azioni. Nella pagina per creare le operazioni, è possibile definire l’esempio di gruppi di utenti in cui verranno eseguite le operazioni e pianificare l’esecuzione dell’operazione in una data futura.

Per creare un&#39;operazione:

1. Definisci il segmento (coorte) da analizzare in una qualsiasi pagina dei rapporti o delle dashboard, utilizzando i passaggi descritti in [Definizione di segmenti e arco temporale](/help/AccountIQ/howto-select-segment-timeframe.md).

1. Seleziona **Crea nuova operazione** disponibile in una qualsiasi delle pagine dei rapporti o delle dashboard. La **Crea nuova operazione** viene visualizzata la pagina .

   ![Pagina per creare una nuova operazione](assets/create-new-operations.png)
   *Figura: Pagina per creare una nuova operazione*

1. Sulla **Crea nuova operazione** compila i dettagli nei campi del modulo per:

   * [Nome operazione](#operation-details) nei dettagli operativi
   * Segmento su cui eseguire l’operazione in [Segmento di destinazione](#segment) e perfeziona il segmento utilizzando [Segmentazione aggiuntiva](#additional-segmentation)
   * [Tipo di segmento](#segment-type) sotto [Segmento di destinazione](#segment)
   * [Azione](#action)
   * [Attivazione della pianificazione](#schedule)

1. [Salva l’operazione](#save-operation).

## Dettagli dell&#39;operazione {#operation-details}

+++Programmatore- dettagli operativi

Denomina la nuova operazione in **Nome operazione** campo in Dettagli operazione. Ad esempio, &quot;*Testa l&#39;effetto dell&#39;autenticazione a più fattori sugli abbonati MVPD X&quot; o &quot;Limita il numero di flussi nel monitoraggio della concorrenza&quot; o &quot;Limita gli abbonati MVPD D che visualizzano il canale &#39;N&#39; da 20 più dispositivi*&quot;.

+++

+++MVPD- dettagli sul funzionamento

Denomina la nuova operazione in **Nome operazione** campo in Dettagli operazione. Ad esempio, &quot;*Testa l&#39;effetto dell&#39;autenticazione a più fattori sui visualizzatori del canale N&quot; o &quot;Limita il numero di flussi nel monitoraggio della concorrenza&quot; o &quot;Limita il canale di visualizzazione degli abbonati &#39;N&#39; da 20 più dispositivi*&quot;.

+++

## Segmento di destinazione {#segment}

+++Programmatore- Segmento di Target

La **Segmento** definisce gli utenti che saranno gestiti da questa operazione; o il gruppo di esempio per l&#39;operazione. Il segmento predefinito è il **segmento** selezionato con [pannello relativo al segmento e al calendario](/help/AccountIQ/howto-select-segment-timeframe.md) nella pagina dei report principali o delle dashboard del passaggio 1 precedente.

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

Questo segmento definisce i sottoscrittori che saranno interessati dall’operazione in fase di creazione. Ad esempio, il segmento selezionato potrebbe specificare *tutti gli account sottoscrittori di MVPD denominato &quot;C&quot; che visualizzano il canale &#39;N Sports&#39;*.

+++

+++MVPD- Segmento di destinazione

La **Segmento** definisce gli utenti che saranno gestiti da questa operazione; o il gruppo di esempio per l&#39;operazione. Il segmento predefinito è il **segmento** selezionato con [pannello relativo al segmento e al calendario](/help/AccountIQ/howto-select-segment-timeframe.md) nella pagina dei report principali o delle dashboard del passaggio 1 precedente.

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

Questo segmento definisce gli abbonati (che sono visualizzatori di canali specifici) che saranno interessati dall’operazione in fase di creazione. Ad esempio, il segmento (predefinito) include *tutti gli account abbonati che visualizzano il canale &#39;N Sport&#39;*.
+++

### Segmentazione aggiuntiva {#additional-segmentation}

Inoltre, puoi perfezionare il segmento di destinazione aggiungendo ulteriori metriche. Ad esempio, puoi aggiungere la probabilità di condivisione maggiore del 90% come un’altra metrica. Quindi, ora la dichiarazione del problema dice *&quot;crea un&#39;operazione per gli account sottoscrittori di MVPD denominato &quot;C&quot; che visualizzano il canale &quot;N Sport&quot; che hanno una probabilità di condivisione maggiore del 90%&quot;*.

![](assets/additional-segment.gif)

*Figura: Segmentazione aggiuntiva*

Inoltre, se si perfeziona l&#39;operazione aggiungendo un&#39;altra metrica per il numero di dispositivi, l&#39;istruzione del problema aggiornata legge *&quot;crea un&#39;operazione per gli account sottoscrittori di MVPD denominato &quot;C&quot; che visualizzano il canale &#39;N Sports&#39; che hanno un punteggio di condivisione superiore a 90 e utilizzano più di 5 dispositivi per visualizzare il contenuto durante il periodo di valutazione&quot;*.

![](assets/refined-segment.png)

*Figura: Segmento di esempio perfezionato con punteggio di condivisione complessivo e metriche del numero di dispositivi*

In questo modo, il gruppo di utenti diventa più preciso. Quindi, aggiungendo più metriche e condizioni, qualifichi ulteriormente il segmento per definire gli account su cui operare.

### Tipo di segmento {#segment-type}

Il tipo di segmento è il modo in cui un segmento viene trattato durante il periodo di valutazione dell’operazione.

![](assets/segment-type.png)

*Figura: Perfezionare il numero di segmenti su cui operare utilizzando il tipo di segmento*

<!--The segment type option allows you to further refine your segment based on the evaluation period (or time).

**Fixed number of accounts** 

When you select **Fixed number of accounts** segment type, then you need to specify an evaluation period as well.

By doing so, you are fixing the sample size for evaluation in terms of numbers. You are making Account IQ identify a specific set of users (that meet the criteria of defined evaluation period and segment metrics) to operate on. The analysis and graphs will be generated for this specific set of users only (identified initially) throughout the operation.

**Variable number of accounts**

When you select **Variable number of accounts** segment type, you do not limit the number of accounts in segment. The accounts which fall under the defined segment metrics are the part of the segment, and the number of accounts will change continuously during the course of operation.-->

>[!IMPORTANT]
>
>Puoi utilizzare solo **Numero fisso di account** a partire da ora. Opzione da selezionare **Numero di conti variabili** saranno disponibili nelle prossime versioni.

<!--

you tell Account IQ in the beginning of the operation which number of accounts to operate on.

Account IQ system only has a segment definition, and during the operation it looks into all the accounts that fit that segments.

the number of accounts in segment is not limited, the accounts that fall under defined segment metrics will be part of the segment, and the no of accounts will change continuously, as there are no specific limitations - like an evaluation period in the past.When the segment is defined (which in this example is, subscriber accounts of MVPD 'C' who are viewing the channel 'N Sports' that have a sharing score above 80 and are using 10 different IPs) and we also identified a time period to evaluate a segment. This identifies X number of accounts as sample (for example 5000). How many devices they are using?
It identifies x-number of accounts (5000)...a very specific set of users that meet this criteria.
for every period that we schedule (within that operation) during that operation) we will look at those 5K users that are originally identified and we will present graph about them. How are the sharing scores coming up?u We identified a period. Are their sharing scores going up? Are there fewer of them who are meeting this definition?
Fixed versus variable is the way the treated in fixed or variable way.

1. we identified a fixed set of accounts.
2. we evaluate those specific accounts on criteria throughout the operation.

General idea independent of graph is that we will evaluate a set of accounts identified initially, for no of periods during operation and generate graphs against that.
Those are the 5000 users for which I will create graphs for for every period of the operation.

**Variable number of accounts**
We do not identify any initial set of accounts, we just have a segment definition.
Each period during the operation, we go and look into all the accounts that fit that segments.
If it is not a fixed segment, I won't initially evaluate it. I won't have an initial set of 5000. Instead at every period during the evaluation I will evaluate the segment then, and then I will produce graph about the next 3000 users.
the......will vary from period to period.

if not fixed segment, then I won't initially evaluate or have initial set of 5000, instead at every period during an operation and the.-->

## Azione {#action}

La **Azione** definisce l’operazione da eseguire sul segmento definito.

Puoi eseguire due tipi di azioni:

* Azioni che utilizzano sistemi integrati con Account IQ; quali **Monitoraggio della concorrenza** <!--[Concurrency Monitoring](https://tve.helpdocsonline.com/concurrency-monitoring-introduction), or Adobe Target-->.

* Azioni per creare ed elaborare flussi di lavoro esterni all&#39;Account IQ e non integrati con il sistema Account IQ. Ad esempio, un&#39;azione per il programmatore di canale &#39;N&#39; per inviare e-mail in blocco a tutti gli abbonati di MVPD &#39;C&#39;.

>[!NOTE]
>
>Creando le operazioni, non solo si specificano le azioni e ne si definisce l’ambito, ma si inizia anche a registrare l’effetto di tali operazioni.

## Pianificazione{#schedule}

Puoi pianificare l’attivazione per l’operazione impostando le date di inizio e di fine.

>[!NOTE]
>
>La data di inizio e la data di fine hanno una granularità identica a quella selezionata per la valutazione durante la definizione del segmento utilizzando **pannello relativo al segmento e al calendario**, al punto 1.
>
>
>Quindi, se hai selezionato la granularità come Settimana, le date di inizio e di fine sono in termini di settimana (ad esempio Settimana 14); se selezioni la granularità come Mese, le date di inizio e di fine sono in mesi.


>[!IMPORTANT]
>
>La data di inizio deve essere successiva al periodo di valutazione e anche successiva alla data corrente. Analogamente, la data di fine deve essere successiva alla data di inizio e alla data corrente.

### Salva l’operazione {#save-operation}

Quando salvi l’operazione, viene visualizzata una schermata di messaggio che informa che il segmento definito in questa operazione viene salvato anche per il futuro. Tuttavia, devi assegnare un nome a questo segmento.

![](assets/save-operation.png)

*Figura: Salva operazione e specifica il nome del segmento*

>[!NOTE]
>
>È consigliabile denominare l’operazione in base all’azione che si sta eseguendo in combinazione con il segmento su cui agirà.

<!--In future you can select this saved segment when defining a segment for your analysis on the main reports page. Moreover, the saved segment is also listed when you create an operation the next time.

![](assets/saved-segment-operations-page.png)

*Figure: Saved segments in segment selector on Create new operations page* 

>[!IMPORTANT]
>
>When creating an operation, if you select a segment that was previously created then you cannot add new metrics to it and refine it.
>
>Adding new metrics creates a new segment, but you cannot modify an existing segment.-->

Dopo aver creato un&#39;operazione, questa verrà eseguita dalla data di inizio alla data di fine specificata.

I dettagli dell&#39;operazione salvata sono visibili sul [Operazioni](/help/AccountIQ/operations.md) pagina.

![](assets/new-operation-created.png)

*Figura: L&#39;operazione appena creata viene elencata nella pagina Operazioni principale*
