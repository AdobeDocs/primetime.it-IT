---
title: Visualizzare i rapporti in modalità isolamento
description: Visualizza i rapporti in modalità isolamento per Xfinity.
exl-id: e7cf24c5-9bfa-48f6-b5c8-20443a976891
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Visualizzazione della condivisione di rapporti in modalità isolamento {#report-isolation-mode}

In modalità Isolamento, gli MVPD (ad esempio, Xfinity) identificano in modo coerente gli abbonati tra i dispositivi, ma identificano i loro abbonati in modo diverso, in base ai programmatori con cui interagiscono. Mentre in modalità standard, gli MVPD identificano costantemente gli abbonati tra i dispositivi, indipendentemente dai programmatori.

Ad esempio, nell&#39;immagine seguente, se un Sottoscrittore B di un MVPD in modalità di isolamento (come Xfinity) accede al contenuto offerto da due programmatori diversi utilizzando lo stesso dispositivo, l&#39;MVPD associa identificatori diversi ai due diversi tentativi di accesso. Quindi, a quei programmatori (L e M nella figura) e a Account IQ, sembra che ci siano due diversi abbonati che accedono al contenuto. Tuttavia, per MVPD standard, se l&#39;utente che accede al contenuto offerto da due programmatori diversi, l&#39;MVPD assocerà un unico identificativo di accesso per entrambi i tentativi di accesso. Gli MVPD (ad esempio, Xfinity) in modalità isolamento non identificano in modo coerente un abbonato anche se l&#39;abbonato utilizza lo stesso dispositivo tra diversi programmatori.

![](assets/isolation-diff-new.png)

*Figura: Modalità di isolamento MVPD identifica quattro abbonati diversi invece di due*

Per gestire la distorsione dei dati (a causa dell&#39;identificazione dello stesso abbonato come diverso in base all&#39;accesso a diversi programmatori), la Modalità Isolamento limita l&#39;attività riportata su un programmatore all&#39;attività solo sulle applicazioni di quel programmatore. Ad esempio, per la modalità di isolamento nell&#39;immagine precedente, il programmatore L vede i dati solo in base all&#39;attività delle identità W e Y, ignorando le identità X e Z.

>[!IMPORTANT]
>
> Il lato negativo è che il programmatore L è privato della condivisione delle informazioni raccolte sugli abbonati A e B a causa di attività con qualsiasi programmatore diverso da L.

In Modalità isolata tutti i calcoli effettuati per ottenere i Punteggi di condivisione e tutte le metriche associate vengono effettuati utilizzando solo l’attività dei dispositivi in streaming dalle applicazioni appartenenti al Programmatore e ai canali selezionati.
I punteggi e le probabilità di condivisione vengono calcolati solo utilizzando il flusso che inizia dai canali selezionati.

Per visualizzare le metriche in modalità isolamento:

1. Seleziona **modo di isolamento** dal **MVPD nel segmento** opzione a discesa e seleziona **Applica selezione**.

   ![](assets/xfinity-in-segment.gif)

   *Figura: Selezione MVPD in modalità Isolamento*

1. Seleziona i canali desiderati dalla **Canali nel segmento** opzione a discesa e seleziona **Applica selezione**. Inoltre, seleziona una [arco temporale](/help/AccountIQ/product-concepts.md#granularity-def).

   >[!IMPORTANT]
   >
   >Poiché la condivisione dell&#39;account è più rilevante quando viene misurata per lo streaming su tutte le applicazioni dei programmatori, vedrai punteggi di condivisione inferiori e alcune variazioni nelle metriche in modalità isolamento.

   ![](assets/aggregate-sharing-isolation.png)

   *Figura: Condivisione di misuratori di probabilità in modalità Isolamento*

   Si noti che i dati sopra riportati mostrano che solo il 6% di tutti gli account sono condivisi; e solo l’8% del contenuto viene consumato da tale 8%. Quindi i canali possono confrontare i loro punteggi in modalità Isolamento con quelli degli altri MVPD. Pertanto, le informazioni ottenute utilizzando la modalità di isolamento devono essere interpretate in modo diverso rispetto agli altri dati.
