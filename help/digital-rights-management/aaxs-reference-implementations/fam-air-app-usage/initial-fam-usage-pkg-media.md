---
title: Contenuto multimediale del pacchetto
description: Contenuto multimediale del pacchetto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Contenuto multimediale del pacchetto {#package-media}

Utilizza la scheda Package Media per creare un pacchetto di contenuti. La sezione Proprietà Packager visualizza le impostazioni Packager immesse nella scheda Preferenze. Per modificare queste impostazioni, passare alla scheda Preferenze, modificare le impostazioni e salvare.

Se si desidera creare un pacchetto di un singolo file FLV o F4V, scegliere **[!UICONTROL Select Single File]** e immettere il percorso completo del file di origine e il percorso completo in cui salvare il file crittografato.

Se si desidera creare un pacchetto di tutti i file di una cartella, scegliere **[!UICONTROL Select Single Folder]** opzione. Specificare la cartella contenente i file di origine. Solo i file nella cartella di input che corrispondono al **[!UICONTROL Input Media File Selection]** I criteri verranno inseriti (i file nelle sottocartelle non vengono inseriti nel pacchetto). Scegli di crittografare [!DNL .flv] file, [!DNL .f4v] o immettere un&#39;espressione regolare personalizzata (ad esempio &quot;.&#42;&quot; crittografa tutti i file nella cartella). I file crittografati verranno salvati nella cartella di output specificata, utilizzando lo stesso nome del file originale.

>[!NOTE]
>
>I percorsi dei file devono fare riferimento ai file disponibili per il server di creazione pacchetti. Se si esegue Gestione Flash Access in un computer diverso da quello del server di creazione pacchetti, è necessario specificare un percorso accessibile dal server (che si trova su un&#39;unità di rete o sul server stesso).

La tabella seguente descrive le preferenze per i file multimediali del pacchetto:

| Preferenza | Descrizione |
|---|---|
| Nome/i file criteri | Seleziona uno o più criteri dall’elenco a discesa da applicare al contenuto. Per selezionare più criteri, tenere premuto CTRL durante la selezione dei criteri. |
| Secondi non crittografati | Specifica il numero di secondi di contenuto non crittografato all&#39;inizio del file. Per crittografare a partire dall&#39;inizio, immettere &quot;0&quot;. |
| Crittografa video | Seleziona questa casella di controllo per crittografare i dati video |
| Livello di crittografia | Se la crittografia video è abilitata, selezionare il livello di crittografia per i dati video. Alta crittografa tutti i dati video. Medium (Medio) e Low (Basso) crittografano in modo selettivo parti del video. (Solo per F4V con video H.264) |
| Crittografa audio | Seleziona questa casella di controllo per crittografare i dati audio |
| Crittografa script | Selezionare questa casella di controllo per crittografare i dati dello script (solo FLV) |
| Proprietà personalizzate | Specifica le proprietà personalizzate da includere nel contenuto del pacchetto. Queste proprietà saranno disponibili per il server licenze al momento del rilascio di una licenza. (Facoltativo) |

Dopo aver selezionato le opzioni di packaging, fare clic su **[!UICONTROL Package Media]** per iniziare a creare il pacchetto dei file.
