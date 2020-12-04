---
seo-title: File delle proprietà di Packager
title: File delle proprietà di Packager
uuid: 156624ec-66f0-4718-8a66-ed04a47f234d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# File proprietà Packager {#packager-properties-file}

Utilizzate il file [!DNL flashaccess-refimpl-packager.properties] per configurare il componente Folder Packager Watched dell&#39;implementazione di riferimento. Come minimo, accertatevi di impostare l&#39;URL del server delle licenze, il certificato del server delle licenze, le credenziali del packager e le opzioni di protezione delle chiavi. Questo file contiene anche il percorso di ciascuna cartella esaminata (packager.watchfolder.source. `n`). Eventuali modifiche apportate ai valori in questo file di proprietà avranno effetto alla successiva esecuzione del packager delle cartelle controllato (il riavvio del server non è richiesto). Tuttavia, se si verifica un errore di configurazione nel packager, il thread del packager delle cartelle controllato verrà chiuso e il server dovrà essere riavviato per riavviare il thread del packager.
