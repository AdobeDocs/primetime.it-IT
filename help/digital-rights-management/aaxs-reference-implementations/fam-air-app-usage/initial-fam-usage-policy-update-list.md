---
title: Elenco degli aggiornamenti dei criteri
description: Elenco degli aggiornamenti dei criteri
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Elenco aggiornamenti criteri {#policy-update-list}

È possibile utilizzare gli elenchi di aggiornamento dei criteri per comunicare le modifiche dei criteri a un server licenze. Se un criterio viene modificato dopo essere stato utilizzato per creare il pacchetto del contenuto, è consigliabile che il server licenze sia a conoscenza della versione più recente del criterio, in modo che tale versione possa essere utilizzata per rilasciare una licenza.

Per creare un elenco di aggiornamento dei criteri per la prima volta, fare clic su **[!UICONTROL Add policies]** per visualizzare tutti i criteri disponibili sul server. Per tutti i criteri aggiornati dopo l’utilizzo per creare pacchetti di contenuto, seleziona il pulsante di scelta **[!UICONTROL update]** .

Se non desideri più utilizzare un criterio per il rilascio di licenze e il criterio è già stato utilizzato per creare pacchetti di contenuto, puoi revocare il criterio. A tale scopo, selezionare il pulsante di scelta **[!UICONTROL revoke]** . Una volta selezionati i criteri desiderati, scegli **[!UICONTROL Create Policy Update List]**. Un file denominato [!DNL PolicyUpdateList.dat] verrà salvato nella directory [!DNL Resources].

Per modificare un elenco di aggiornamento dei criteri esistente, fare clic su **[!UICONTROL Add policies]** per visualizzare tutti i criteri disponibili sul server. Scegliere i criteri aggiuntivi da aggiungere o revocare. Le voci esistenti nell&#39;elenco degli aggiornamenti dei criteri possono essere modificate nella sezione superiore della schermata. I criteri contrassegnati come **[!UICONTROL updated]** possono essere modificati in **[!UICONTROL revoked]**, ma una volta che un criterio è **[!UICONTROL revoked]** non può essere modificato in **[!UICONTROL updated]**.

Una volta apportate le modifiche desiderate, scegli **[!UICONTROL Create Policy Update List]** e il file [!DNL PolicyUpdateList.dat] viene rigenerato. Se un criterio si trova già nell’elenco di aggiornamento dei criteri ed è stato aggiornato dopo l’ultima generazione dell’elenco, la versione più recente del criterio verrà utilizzata al momento della generazione dell’elenco di aggiornamento dei criteri.
