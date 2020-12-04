---
seo-title: Elenco aggiornamenti criteri
title: Elenco aggiornamenti criteri
uuid: ecc74b66-5b53-4ec3-9641-8b78929e2932
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Elenco aggiornamenti criteri {#policy-update-list}

È possibile utilizzare gli elenchi degli aggiornamenti dei criteri per comunicare le modifiche dei criteri a un server licenze. Se un criterio viene modificato dopo che è stato utilizzato per creare il pacchetto del contenuto, è consigliabile che il server licenze sia a conoscenza della versione più recente del criterio, in modo che tale versione possa essere utilizzata per rilasciare una licenza.

Per creare un elenco di aggiornamento criteri per la prima volta, fare clic su **[!UICONTROL Add policies]** per visualizzare tutti i criteri disponibili sul server. Per tutti i criteri che sono stati aggiornati dopo essere stati utilizzati per creare pacchetti di contenuto, fate clic sul pulsante di scelta **[!UICONTROL update]**.

Se non desiderate più utilizzare un criterio per rilasciare licenze e il criterio è già stato utilizzato per creare pacchetti di contenuto, potete revocare il criterio. A tal fine, selezionare il pulsante di scelta **[!UICONTROL revoke]**. Quando i criteri desiderati sono stati selezionati, scegliere **[!UICONTROL Create Policy Update List]**. Un file denominato [!DNL PolicyUpdateList.dat] verrà salvato nella directory [!DNL Resources].

Per modificare un elenco di aggiornamento criteri esistente, fare clic su **[!UICONTROL Add policies]** per visualizzare tutti i criteri disponibili sul server. Scegliere i criteri aggiuntivi da aggiungere o revocare. Le voci esistenti nell&#39;Elenco aggiornamento criteri possono essere modificate nella sezione superiore della schermata. I criteri contrassegnati come **[!UICONTROL updated]** possono essere modificati in **[!UICONTROL revoked]**, ma una volta che un criterio è **[!UICONTROL revoked]** non può essere cambiato in **[!UICONTROL updated]**.

Quando sono state apportate le modifiche desiderate, scegliete **[!UICONTROL Create Policy Update List]** e il file [!DNL PolicyUpdateList.dat] viene rigenerato. Se un criterio è già presente nell&#39;elenco di aggiornamento dei criteri ed è stato aggiornato dall&#39;ultima generazione dell&#39;elenco, la versione più recente del criterio verrà utilizzata al momento della generazione dell&#39;elenco di aggiornamento dei criteri.
