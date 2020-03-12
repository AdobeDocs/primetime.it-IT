---
description: 'null'
seo-description: 'null'
seo-title: Informazioni sui file di configurazione degli strumenti della riga di comando
title: Informazioni sui file di configurazione degli strumenti della riga di comando
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155

---


# Informazioni sui file di configurazione degli strumenti della riga di comando{#about-command-line-tools-configuration-files}

Gli strumenti della riga di comando vengono visualizzati [!DNL flashaccesstools.properties] nella directory in cui vengono eseguiti gli strumenti. Tuttavia, è possibile utilizzare l&#39; `-c` opzione quando si esegue uno strumento della riga di comando per specificare una posizione diversa per l&#39;impostazione predefinita [!DNL flashaccesstools.properties]. Potete inoltre utilizzare `-c` per specificare un file di configurazione diverso.

I file di configurazione degli strumenti della riga di comando utilizzano il formato di file *delle proprietà* Java, per il quale si applicano le regole seguenti:

* Sbarra rovesciata con una barra rovesciata aggiuntiva.

   Ad esempio, in un computer Windows, per specificare il [!DNL C:\credentials.pfx] file è necessario immetterlo come [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Per specificare un file su un server di rete Windows, è necessario immettere `\\\\server\\folder\\filename.pfx`
* Solo caratteri *Latin-1* .

   Per utilizzare caratteri non *latini-1* , è necessario utilizzare la sequenza di escape Unicode appropriata. Facoltativamente, potete applicare lo [!DNL native2ascii] strumento (incluso in Java) alle voci del file di configurazione.
