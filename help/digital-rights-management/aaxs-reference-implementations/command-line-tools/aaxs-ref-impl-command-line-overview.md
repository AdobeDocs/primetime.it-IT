---
seo-title: 'Strumenti della riga di comando per la creazione di pacchetti di contenuti e di elenchi di revoche '
title: 'Strumenti della riga di comando per la creazione di pacchetti di contenuti e di elenchi di revoche '
uuid: 2c740521-2004-4320-88e1-118b84e80e31
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Strumenti della riga di comando per la creazione di pacchetti di contenuti e di elenchi di revoche {#command-line-tools-for-packaging-content-revocation-lists}

L&#39;implementazione di riferimento include i seguenti strumenti della riga di comando:

* Policy Manager: Uno strumento per la creazione e la gestione dei criteri
* Gestione elenco aggiornamenti criteri: Uno strumento per creare e visualizzare gli elenchi di aggiornamento dei criteri
* Gestione elenco revoca: Uno strumento per creare e visualizzare elenchi di revoche
* Media Packager: Strumento per la creazione di file FLV e F4V crittografati
* ID editore AIR
* UtilityLicense Generator
* Embedder licenza

## Requisiti {#requirements}

I requisiti per l&#39;utilizzo degli strumenti della riga di comando disponibili nelle implementazioni di riferimento sono i seguenti:

* Tutti gli strumenti della riga di comando richiedono Java 1.5 o versione successiva.
* Credenziali Packager e License Server (certificato e password) emesse dal Adobe . Per crittografare e firmare i file video, per firmare gli elenchi Aggiornamento e Revoca criteri e per pregenerare le licenze sono necessarie delle credenziali.

>[!NOTE]
>
>A causa di un bug Java, gli argomenti utilizzati sulla riga di comando (quali nomi di file, nomi di criteri o descrizioni) devono utilizzare solo caratteri del set di caratteri predefinito del sistema operativo.

## File di configurazione {#configuration-file}

Diversi strumenti della riga di comando richiedono un file di configurazione contenente informazioni relative agli strumenti da utilizzare per l&#39;applicazione di criteri e la cifratura dei file.

Il file di configurazione predefinito è [!DNL flashaccesstools.properties]. si trova nella directory di lavoro; ovvero la directory da cui vengono eseguiti gli strumenti (vedere Installazione degli strumenti della riga di comando). Ogni strumento contiene anche un&#39;opzione ( `-c`) che consente di puntare al file di configurazione che si desidera utilizzare se si preferisce non utilizzare il valore predefinito.

Il file di configurazione utilizza il formato di file delle proprietà Java. Se i valori di una delle proprietà contengono caratteri speciali, tenere presente le seguenti limitazioni:

* Sbarra rovesciata con una barra rovesciata aggiuntiva. Ad esempio, per specificare il file [!DNL C:\credentials.pfx], specificarlo come [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Per specificare un file su un server di rete, specificare `\\\\server\\folder\\filename.pfx`.
* Il file di configurazione può contenere solo caratteri Latin-1. Se è necessario utilizzare caratteri non latini-1, utilizzare la sequenza di escape Unicode appropriata (utilizzando, facoltativamente, lo strumento [!DNL native2ascii] fornito con Java).

Impostate i valori delle proprietà nel file di configurazione prima di eseguire gli strumenti. Per alcuni strumenti della riga di comando, è possibile impostare i valori di alcune opzioni tramite la riga di comando o il file di configurazione. In questi casi, i valori impostati tramite la riga di comando hanno la precedenza su qualsiasi valore presente nel file di configurazione.

## Installazione degli strumenti della riga di comando {#installing-the-command-line-tools}

È possibile copiare i file necessari dalla directory [!DNL \Reference Implementation\Command Line Tools] del DVD, che contiene il file di configurazione [!DNL flashaccesstools.properties] predefinito, e una directory [!DNL libs], che contiene i file JAR per gli strumenti.

La directory [!DNL samples] contiene diversi file sorgente Java di esempio che dimostrano l&#39;utilizzo delle API SDK di accesso al Adobe . Per creare ed eseguire gli esempi, utilizzare lo script [!DNL build-samples.xml] Ant.