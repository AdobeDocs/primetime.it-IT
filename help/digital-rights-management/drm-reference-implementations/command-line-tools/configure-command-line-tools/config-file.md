---
title: Informazioni sui file di configurazione degli strumenti della riga di comando
description: Informazioni sui file di configurazione degli strumenti della riga di comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Informazioni sui file di configurazione degli strumenti della riga di comando{#about-command-line-tools-configuration-files}

Gli strumenti della riga di comando cercano [!DNL flashaccesstools.properties] nella directory in cui vengono eseguiti gli strumenti. Tuttavia, è possibile utilizzare `-c` quando si esegue uno strumento da riga di comando per specificare una posizione diversa per il valore predefinito [!DNL flashaccesstools.properties]. Puoi anche utilizzare `-c` per specificare un file di configurazione diverso.

I file di configurazione degli strumenti della riga di comando utilizzano *File di proprietà Java* formato, al quale si applicano le seguenti regole:

* Esci dalle barre rovesciate con una barra rovesciata aggiuntiva.

  Ad esempio, in un computer Windows per specificare [!DNL C:\credentials.pfx] file, è necessario immetterlo come [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Per specificare un file in un server di rete Windows, è necessario immettere `\\\\server\\folder\\filename.pfx`
* Solo inclusione *Latin-1* caratteri.

  Per utilizzare non *Latin-1* caratteri, è necessario utilizzare la sequenza di escape Unicode appropriata. Facoltativamente, puoi applicare [!DNL native2ascii] (incluso in Java) alle voci del file di configurazione.
