---
title: Strumenti della riga di comando per creare pacchetti di contenuto e creare elenchi di revoche
description: Strumenti della riga di comando per creare pacchetti di contenuto e creare elenchi di revoche
copied-description: true
exl-id: 34305dab-a2f0-41c2-9a59-3261e8dea7e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Strumenti della riga di comando per creare pacchetti di contenuto e creare elenchi di revoche {#command-line-tools-for-packaging-content-revocation-lists}

L’implementazione di riferimento include i seguenti strumenti della riga di comando:

* Policy Manager: strumento per la creazione e la gestione delle policy
* Policy Update List Manager: strumento per la creazione e la visualizzazione di elenchi di aggiornamento dei criteri
* Revocation List Manager: strumento per la creazione e la visualizzazione di elenchi di revoca
* Media Packager: strumento per la creazione di file FLV e F4V crittografati
* ID editore AIR
* UtilityLicense Generator
* Incorporatore licenza

## Requisiti {#requirements}

I requisiti per l’utilizzo degli strumenti della riga di comando disponibili nelle implementazioni di riferimento sono i seguenti:

* Tutti gli strumenti della riga di comando richiedono Java 1.5 o versione successiva.
* Credenziali Packager e License Server (certificato e password) rilasciate da Adobe. Sono necessarie credenziali per crittografare e firmare file video, per firmare elenchi di aggiornamento e revoca della policy e per pregenerare licenze.

>[!NOTE]
>
>A causa di un bug Java, gli argomenti utilizzati nella riga di comando (ad esempio nomi di file, nomi di criteri o descrizioni) devono utilizzare solo caratteri del set di caratteri predefinito del sistema operativo.

## File di configurazione {#configuration-file}

Diversi strumenti della riga di comando richiedono un file di configurazione contenente informazioni che gli strumenti devono utilizzare per l&#39;applicazione delle policy e la crittografia dei file.

Il file di configurazione predefinito è [!DNL flashaccesstools.properties]. Si trova nella directory di lavoro, ovvero la directory da cui vengono eseguiti gli strumenti (vedere Installazione degli strumenti della riga di comando). Ogni strumento contiene anche un&#39;opzione ( `-c`) che consente di selezionare il file di configurazione da utilizzare se si preferisce non utilizzare l&#39;impostazione predefinita.

Il file di configurazione utilizza il formato di file delle proprietà Java. Se i valori di una qualsiasi delle proprietà contengono caratteri speciali, tieni presente le seguenti restrizioni:

* Esci dalle barre rovesciate con una barra rovesciata aggiuntiva. Ad esempio, per specificare [!DNL C:\credentials.pfx] file, specificalo come [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Per specificare un file su un server di rete, specificare `\\\\server\\folder\\filename.pfx`.
* Il file di configurazione può contenere solo caratteri Latin-1. Se è necessario utilizzare caratteri diversi da Latin-1, utilizzare la sequenza di escape Unicode appropriata (facoltativamente, utilizzando [!DNL native2ascii] Java).

Impostare i valori per le proprietà nel file di configurazione prima di eseguire gli strumenti. Per alcuni strumenti della riga di comando, è possibile impostare i valori di alcune opzioni tramite la riga di comando o il file di configurazione. In questi casi, i valori impostati tramite la riga di comando hanno la precedenza su qualsiasi valore nel file di configurazione.

## Installazione degli strumenti della riga di comando  {#installing-the-command-line-tools}

È possibile copiare i file necessari da [!DNL \Reference Implementation\Command Line Tools] sul DVD, che contiene la directory predefinita [!DNL flashaccesstools.properties] e un file di configurazione [!DNL libs] , che contiene i file JAR per gli strumenti.

Il [!DNL samples] La directory contiene diversi file Java di origine di esempio che illustrano l’utilizzo delle API SDK di Adobe Access. Per generare ed eseguire gli esempi, utilizzare [!DNL build-samples.xml] Script di formica.
