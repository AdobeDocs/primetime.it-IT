---
title: Elenco aggiornamenti criteri
description: Elenco aggiornamenti criteri
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Elenco aggiornamenti criteri {#policy-update-list}

È possibile utilizzare gli elenchi di aggiornamento dei criteri per comunicare le modifiche dei criteri a un server licenze. Se un criterio viene modificato dopo essere stato utilizzato per creare un pacchetto di contenuto, è consigliabile che il server licenze conosca la versione più recente del criterio, in modo che tale versione possa essere utilizzata per rilasciare una licenza.

Per creare un elenco di aggiornamento dei criteri per la prima volta, fare clic su **[!UICONTROL Add policies]** per visualizzare tutti i criteri disponibili sul server. Per tutti i criteri aggiornati da quando sono stati utilizzati per creare pacchetti di contenuto, seleziona la **[!UICONTROL update]** pulsante di opzione.

Se non desideri più utilizzare un criterio per rilasciare licenze e il criterio è già stato utilizzato per creare pacchetti di contenuto, puoi revocare il criterio. A questo scopo, seleziona la **[!UICONTROL revoke]** pulsante di opzione. Dopo aver selezionato i criteri desiderati, scegli **[!UICONTROL Create Policy Update List]**. Un file denominato [!DNL PolicyUpdateList.dat] verrà salvato in [!DNL Resources] Directory.

Per modificare un elenco di aggiornamento dei criteri esistente, fare clic su **[!UICONTROL Add policies]** per visualizzare tutti i criteri disponibili sul server. Scegli i criteri aggiuntivi da aggiungere o revocare. Le voci esistenti nell’Elenco di aggiornamento dei criteri possono essere modificate nella sezione superiore della schermata. Criteri contrassegnati **[!UICONTROL updated]** può essere modificato in **[!UICONTROL revoked]**, ma una volta che una policy è **[!UICONTROL revoked]**, non può essere ripristinato a **[!UICONTROL updated]**.

Dopo aver apportato le modifiche desiderate, scegli **[!UICONTROL Create Policy Update List]** e [!DNL PolicyUpdateList.dat] viene rigenerato. Se un criterio è già presente nell&#39;elenco di aggiornamento dei criteri ed è stato aggiornato dall&#39;ultima volta che l&#39;elenco è stato generato, quando l&#39;elenco di aggiornamento dei criteri viene nuovamente generato verrà utilizzata la versione più recente del criterio.
