---
title: Operazioni nel IQ account
description: Le operazioni nell'IQ account comportano azioni per eseguire automatizzazioni e operazioni in blocco sugli account degli abbonati e per tracciarne gli effetti.
source-git-commit: e61cca77bad4f01de871e300dc99d7368c283f2a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Operazioni {#operations-tab-next-steps}

Una volta compresi i pattern di utilizzo degli abbonati e identificato la condivisione della password per un segmento selezionato (utilizzando reporting e analisi in Account IQ), puoi intraprendere azioni mirate per un obiettivo di mitigare la condivisione delle password.

La funzionalità Operazioni in Account IQ consente di gestire e gestire in modo efficace la condivisione delle credenziali tramite procedure mirate, denominate operazioni. Offre le opzioni per progettare azioni mirate oggettive e personalizzate (in base all’obiettivo) per specifici gruppi di account di abbonati e automatizzarne l’esecuzione per una durata futura. La funzionalità Operazioni consente non solo di creare ed eseguire operazioni, ma anche di misurarne l’impatto. Quindi, misurando gli impatti è possibile regolare la strategia per ottimizzare l&#39;effetto, sia che si tratti di convertire i mutuatari o di mitigare la condivisione delle credenziali.

Per visualizzare **Operazioni** selezione pagina **Operazioni** opzione sotto **Azioni** nella navigazione a sinistra dell&#39;applicazione Account IQ. Nella pagina Operazioni sono elencate tutte le operazioni già esistenti nel sistema IQ account e i relativi dettagli.

![](assets/operations-page.png)

*Figura: Elenco e dettagli delle operazioni esistenti in Account IQ*

Nella pagina Operazioni è possibile:

* Visualizza un elenco delle operazioni già esistenti in Account IQ

* Visualizzare i dettagli dell’operazione, ad esempio:

   * stato (Pianificato, In esecuzione, Terminato, Errore o Interrotto)

   * progressi (in percentuale di completamento)

   * pubblico target (segmento su cui eseguire l’operazione)

   * pianificazione (data di inizio e di fine del funzionamento)

   * creazione e data di fine dell&#39;operazione

* [Crea nuova operazione](/help/AccountIQ/operation-affecting-user-segment.md)

* [Visualizzare i rapporti sulle operazioni](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## Visualizzare i rapporti sulle operazioni {#operation-reports}

Puoi analizzare l’impatto di un’operazione visualizzandone il rapporto. Per visualizzare il rapporto di un&#39;operazione:

1. Selezionare il nome dell&#39;operazione nella pagina Operazioni principale.

   Il rapporto viene visualizzato sotto forma di grafico a barre sovrapposte.

   ![](assets/operation-impact-report.png)

   *Figura: Rapporto sulle operazioni per visualizzare gli impatti delle operazioni*

   L&#39;asse x traccia il periodo di valutazione e l&#39;asse y traccia una variabile per misurare l&#39;impatto dell&#39;operazione.

   Ad esempio, nell’immagine precedente la variabile sull’asse y è il numero di account. Osservando il grafico è possibile confrontare il numero di conti che si trovano nel segmento delle operazioni rispetto al numero di conti che si trovano al di fuori del segmento delle operazioni in un dato momento (ad esempio la seconda settimana del periodo di valutazione delle operazioni). Pertanto, puoi analizzare come nel periodo di valutazione il numero di account varia all’interno del segmento di operazione e all’esterno del segmento.

   Quindi, se l&#39;operazione consisteva nell&#39;inviare e-mail di avviso a account sospetti e gli account nel segmento delle operazioni erano quelli con probabilità di condivisione superiore a 90 e che utilizzavano più di 5 dispositivi per lo streaming dei contenuti, all&#39;inizio del periodo di valutazione gli account nel segmento sono più di 7 milioni. Questo numero cambia nel corso del periodo di valutazione, come mostrato nel grafico, indicando in tal modo l&#39;impatto dell&#39;operazione. In base alla valutazione, puoi prendere misure correttive su account sospetti o continuare con l’operazione, oppure modificare la strategia per risultati migliori per limitare la condivisione delle credenziali.

2. Per chiudere il rapporto e tornare alla pagina Operazioni principale, selezionare **Operazioni** opzione sotto **Azioni** nella navigazione a sinistra.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->