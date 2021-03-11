---
title: Informazioni sui file di configurazione degli strumenti della riga di comando
description: Informazioni sui file di configurazione degli strumenti della riga di comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Informazioni sui file di configurazione degli strumenti della riga di comando{#about-command-line-tools-configuration-files}

Gli strumenti della riga di comando cercano [!DNL flashaccesstools.properties] nella directory in cui vengono eseguiti gli strumenti. Tuttavia, è possibile utilizzare l&#39;opzione `-c` quando si esegue uno strumento a riga di comando per specificare una posizione diversa per il percorso predefinito [!DNL flashaccesstools.properties]. È inoltre possibile utilizzare `-c` per specificare un file di configurazione diverso.

I file di configurazione degli strumenti della riga di comando utilizzano il formato *file di proprietà Java*, per il quale si applicano le seguenti regole:

* Elimina le barre rovesciate con una barra rovesciata aggiuntiva.

   Ad esempio, su un computer Windows, per specificare il file [!DNL C:\credentials.pfx], è necessario immetterlo come [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Per specificare un file su un server di rete Windows, è necessario immettere `\\\\server\\folder\\filename.pfx`
* Includere solo caratteri *Latin-1*.

   Per utilizzare caratteri non-*Latin-1*, è necessario utilizzare la sequenza di escape Unicode appropriata. Facoltativamente, puoi applicare lo strumento [!DNL native2ascii] (incluso con Java) alle voci del file di configurazione.
