---
title: Supporti pacchetto
description: Supporti pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Supporti pacchetto {#package-media}

Utilizza la scheda File multimediali pacchetto per creare un pacchetto del contenuto. Nella sezione Proprietà del Packager vengono visualizzate le impostazioni del Packager immesse nella scheda Preferenze. Per modificare queste impostazioni, vai alla scheda Preferenze, modifica le impostazioni e salva.

Se desideri creare un pacchetto per un singolo file FLV o F4V, scegli l&#39;opzione **[!UICONTROL Select Single File]** e immetti il percorso completo del file di origine e il percorso completo in cui salvare il file crittografato.

Se desideri creare un pacchetto con tutti i file presenti in una cartella, scegli l’opzione **[!UICONTROL Select Single Folder]** . Specifica la cartella contenente i file di origine. Solo i file nella cartella di input che corrispondono ai criteri **[!UICONTROL Input Media File Selection]** verranno inseriti in un pacchetto (i file nelle sottocartelle non vengono inseriti in un pacchetto). Scegli di crittografare i file [!DNL .flv], i file [!DNL .f4v] o immetti un&#39;espressione regolare personalizzata (ad esempio &quot;.*&quot; crittografa tutti i file nella cartella). I file crittografati verranno salvati nella cartella di output specificata, utilizzando lo stesso nome file del file originale.

>[!NOTE]
>
>I percorsi dei file devono fare riferimento ai file disponibili per il server di packaging. Se si esegue Gestione Flash Access su un computer diverso dal server di packaging, è necessario specificare un percorso accessibile dal server (che si trova su un&#39;unità di rete o sul server stesso).

La tabella seguente descrive le preferenze per i file multimediali pacchetto:

| Preferenza | Descrizione |
|---|---|
| Nome/i file dei criteri | Seleziona uno o più criteri dall’elenco a discesa da applicare al contenuto. Per selezionare più criteri, tenere premuto il tasto CTRL durante la selezione dei criteri. |
| Secondi non crittografati | Specifica il numero di secondi di contenuto da lasciare non crittografato all’inizio del file. Per crittografare a partire dall&#39;inizio, immetti &quot;0&quot;. |
| Cifratura video | Seleziona questa casella di controllo per crittografare i dati video |
| Livello di crittografia | Se la crittografia video è abilitata, selezionare il livello di crittografia per i dati video. La codifica elevata di tutti i dati video. Le parti del video crittografate in modo selettivo medio e basso. (Solo per F4V con video H.264) |
| Cifra audio | Selezionare questa casella di controllo per crittografare i dati audio |
| Crittografa script | Selezionare questa casella di controllo per crittografare i dati di script (solo FLV) |
| Proprietà personalizzate | Specifica le proprietà personalizzate da includere nel contenuto del pacchetto. Queste proprietà saranno disponibili per il server licenze al momento del rilascio di una licenza. (Facoltativo) |

Dopo aver selezionato le opzioni di imballaggio, fai clic sul pulsante **[!UICONTROL Package Media]** per iniziare a creare il pacchetto dei file.
