---
seo-title: Supporti pacchetto
title: Supporti pacchetto
uuid: f6e877be-d916-4766-bc44-99891a3df3a8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Supporti pacchetto {#package-media}

Utilizzate la scheda Pacchetto multimediale per creare pacchetti di contenuto. Nella sezione Proprietà di Packager sono visualizzate le impostazioni di Packager immesse nella scheda Preferenze. Per modificare queste impostazioni, passate alla scheda Preferenze, modificate le impostazioni e selezionate Salva.

Se desiderate creare un pacchetto per un singolo file FLV o F4V, scegliete l&#39;opzione **[!UICONTROL Select Single File]** e immettete il percorso completo del file di origine e il percorso completo in cui salvare il file crittografato.

Se desiderate creare un pacchetto per tutti i file in una cartella, scegliete l&#39;opzione **[!UICONTROL Select Single Folder]**. Specificate la cartella che contiene i file sorgente. Solo i file nella cartella di input che corrispondono ai criteri **[!UICONTROL Input Media File Selection]** saranno inclusi nel pacchetto (i file nelle sottocartelle non vengono inclusi nel pacchetto). Scegliere di cifrare [!DNL .flv] file, [!DNL .f4v] file o immettere un&#39;espressione regolare personalizzata (ad esempio &quot;.*&quot; codifica tutti i file nella cartella). I file crittografati verranno salvati nella cartella di output specificata, utilizzando lo stesso nome file del file originale.

>[!NOTE]
>
>I percorsi dei file devono fare riferimento ai file disponibili per il server di creazione pacchetti. Se si esegue Gestione Flash Access su un computer diverso dal server di creazione pacchetti, è necessario specificare un percorso accessibile dal server (che si trova su un&#39;unità di rete o sul server stesso).

Nella tabella seguente sono descritte le preferenze per i file multimediali pacchetto:

| Preferenza | Descrizione |
|---|---|
| Nome/i file criteri | Selezionare uno o più criteri dall&#39;elenco a discesa da applicare al contenuto. Per selezionare più criteri, tenere premuto il tasto CTRL durante la selezione dei criteri. |
| Secondi non crittografati | Specifica il numero di secondi di contenuto da lasciare non crittografato all&#39;inizio del file. Per eseguire la cifratura a partire dall&#39;inizio, immettere &quot;0&quot;. |
| Cifra video | Selezionate questa casella di controllo per cifrare i dati video |
| Livello crittografia | Se la cifratura video è attivata, selezionate il livello di cifratura per i dati video. Elevata codifica tutti i dati video. Le proprietà Medium e Low (Media e Bassa) crittografano in modo selettivo parti del video. (Solo per F4V con video H.264) |
| Cifra audio | Selezionate questa casella di controllo per cifrare i dati audio |
| Crittografa script | Selezionare questa casella di controllo per cifrare i dati di script (solo FLV) |
| Proprietà personalizzate | Specificate le proprietà personalizzate da includere nel contenuto del pacchetto. Queste proprietà saranno disponibili per il server licenze al momento del rilascio di una licenza. (Facoltativo) |

Dopo aver selezionato le opzioni di pacchetto, fate clic sul pulsante **[!UICONTROL Package Media]** per iniziare a creare il pacchetto dei file.
