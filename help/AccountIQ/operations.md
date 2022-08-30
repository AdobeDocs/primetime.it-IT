---
title: Operazioni nel IQ account
description: Le operazioni nell'IQ account comportano azioni per eseguire automatizzazioni e operazioni in blocco sugli account degli abbonati e per tracciarne gli effetti.
exl-id: ba6bceca-221c-42db-b207-804e4b9f6d54
source-git-commit: 40239b6715d8eab95bc2564fb19eb6832387ad3e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Operazioni {#operations-tab-next-steps}

Una volta compresi i pattern di utilizzo degli abbonati e identificato la condivisione della password per un segmento selezionato (utilizzando reporting e analisi in Account IQ), puoi intraprendere azioni mirate per un obiettivo di mitigare la condivisione delle password.

La funzionalità Operazioni in Account IQ consente di gestire e gestire in modo efficace la condivisione delle credenziali tramite procedure mirate, denominate operazioni. Offre le opzioni per progettare azioni mirate oggettive e personalizzate (in base all’obiettivo) per specifici gruppi di account di abbonati e automatizzarne l’esecuzione per una durata futura. La funzionalità Operazioni consente non solo di creare ed eseguire operazioni, ma anche di misurarne l’impatto. Quindi, misurando gli impatti è possibile regolare la strategia per ottimizzare l&#39;effetto, sia che si tratti di convertire i mutuatari o di mitigare la condivisione delle credenziali.

Per visualizzare **Operazioni** selezione pagina **Operazioni** opzione sotto **Azioni** nella navigazione a sinistra dell&#39;applicazione Account IQ. Nella pagina Operazioni sono elencate tutte le operazioni già esistenti nel sistema IQ dell&#39;account, insieme ai relativi dettagli.

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

   L&#39;asse X rappresenta il periodo di valutazione e l&#39;asse y rappresenta l&#39;impatto dell&#39;operazione (in termini di numero di conti in un segmento durante il periodo di valutazione). Ogni barra è divisa in tre parti.

   * Una parte rappresenta il numero di account che soddisfano ancora i criteri del segmento di operazione.

   * Un&#39;altra parte rappresenta il numero di account attivi per quel periodo che erano originariamente nel segmento, ma non soddisfano più i criteri del segmento di operazione.

   * La terza parte rappresenta i conti che non erano attivi in quel periodo.
   >[!NOTE]
   >
   >La prima barra rappresenta il numero di conti che soddisfano le condizioni del segmento dell&#39;operazione all&#39;inizio del periodo di valutazione.

   Nel tempo il grafico mostra l’effetto dell’azione (tramite l’operazione) indicando il numero di account che hanno modificato il loro comportamento rispetto ai criteri originali (ad esempio, con una probabilità di condivisione superiore a 90 e utilizzando più di 5 dispositivi) o che sono diventati inattivi.

<!--For example, in the above image the variable on the y-axis is number of accounts. Looking at the graph you can compare the number of accounts that are in the operations' segment versus the number of accounts that are outside the operations segment at a particular time (such as week 2nd of the operations evaluation period). Therefore, you can analyze how over the evaluation period do number of accounts vary within the operation segment and outside the segment.

So, if your operation was to send out warning emails to suspecting accounts, and accounts in operations segment were those with sharing probability more than 90 and using more than 5 devices to stream content, then in the beginning of the evaluation period accounts in segment are more than 17 thousand. This number changes over the evaluation period as shown in the graph, thereby indicating the impact of operation. Based on the evaluation, you can take remedial measures on suspecting accounts, or continue with the operation, or adjust your strategy for better outcomes to curb credential sharing.-->

1. Per chiudere il rapporto e tornare alla pagina Operazioni principale, selezionare **Operazioni** opzione sotto **Azioni** nella navigazione a sinistra.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->