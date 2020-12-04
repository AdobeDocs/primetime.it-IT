---
description: 'null'
seo-description: 'null'
seo-title: Informazioni sui file di configurazione degli strumenti della riga di comando
title: Informazioni sui file di configurazione degli strumenti della riga di comando
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Informazioni sui file di configurazione degli strumenti della riga di comando{#about-command-line-tools-configuration-files}

Gli strumenti della riga di comando si trovano nella directory in cui vengono eseguiti gli strumenti. [!DNL flashaccesstools.properties] Tuttavia, è possibile utilizzare l&#39;opzione `-c` quando si esegue uno strumento della riga di comando per specificare una posizione diversa per il percorso predefinito [!DNL flashaccesstools.properties]. È inoltre possibile utilizzare `-c` per specificare un file di configurazione diverso.

I file di configurazione degli strumenti della riga di comando utilizzano il formato *file di proprietà Java*, per il quale si applicano le regole seguenti:

* Sbarra rovesciata con una barra rovesciata aggiuntiva.

   Ad esempio, su un computer Windows, per specificare il file [!DNL C:\credentials.pfx] è necessario immetterlo come [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Per specificare un file su un server di rete Windows, è necessario immettere `\\\\server\\folder\\filename.pfx`
* Includere solo caratteri *Latin-1*.

   Per utilizzare caratteri non-*Latin-1*, è necessario utilizzare la sequenza di escape Unicode appropriata. Facoltativamente, potete applicare lo strumento [!DNL native2ascii] (incluso con Java) alle voci del file di configurazione.
