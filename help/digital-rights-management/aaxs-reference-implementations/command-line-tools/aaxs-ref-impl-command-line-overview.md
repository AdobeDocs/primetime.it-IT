---
title: 'Strumenti da riga di comando per la creazione di pacchetti di contenuti e di elenchi di revoche '
description: 'Strumenti da riga di comando per la creazione di pacchetti di contenuti e di elenchi di revoche '
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Strumenti da riga di comando per la creazione di pacchetti di contenuti e di elenchi di revoche {#command-line-tools-for-packaging-content-revocation-lists}

L’implementazione di riferimento include i seguenti strumenti della riga di comando:

* Responsabile criteri: Strumento per la creazione e la gestione dei criteri
* Gestione elenco aggiornamenti criteri: Strumento per la creazione e la visualizzazione degli elenchi di aggiornamento dei criteri
* Gestione elenco revoche: Strumento per la creazione e la visualizzazione degli elenchi di revoche
* Pacchetto multimediale: Strumento per la creazione di file FLV e F4V crittografati
* ID editore AIR
* UtilityLicense Generator
* Embedder licenza

## Requisiti {#requirements}

I requisiti per l’utilizzo degli strumenti della riga di comando disponibili nelle implementazioni di riferimento sono i seguenti:

* Tutti gli strumenti della riga di comando richiedono Java 1.5 o versioni successive.
* Credenziali del Packager e del server licenze (certificato e password) emesse da Adobe. È necessario disporre di credenziali per crittografare e firmare i file video, per firmare gli elenchi di aggiornamento e revoca dei criteri e per pregenerare le licenze.

>[!NOTE]
>
>A causa di un bug Java, gli argomenti utilizzati nella riga di comando (ad esempio nomi di file, nomi di criteri o descrizioni) devono utilizzare solo caratteri del set di caratteri predefinito del sistema operativo.

## File di configurazione {#configuration-file}

Molti degli strumenti della riga di comando richiedono un file di configurazione contenente informazioni sugli strumenti da utilizzare per l&#39;applicazione dei criteri e la crittografia dei file.

Il file di configurazione predefinito è [!DNL flashaccesstools.properties]. si trova nella directory di lavoro; ovvero la directory da cui vengono eseguiti gli strumenti (vedere Installazione degli strumenti della riga di comando). Ogni strumento contiene anche un&#39;opzione ( `-c`) che consente di puntare al file di configurazione che si desidera utilizzare se si preferisce non utilizzare il valore predefinito.

Il file di configurazione utilizza il formato di file delle proprietà Java. Se i valori di una delle proprietà contengono caratteri speciali, tenere presente le seguenti restrizioni:

* Elimina le barre rovesciate con una barra rovesciata aggiuntiva. Ad esempio, per specificare il file [!DNL C:\credentials.pfx], specificalo come [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Per specificare un file su un server di rete, specificare `\\\\server\\folder\\filename.pfx`.
* Il file di configurazione può contenere solo caratteri latini-1. Se è necessario utilizzare caratteri non latini-1, utilizzare la sequenza di escape Unicode appropriata (utilizzando, facoltativamente, lo strumento [!DNL native2ascii] fornito con Java).

Imposta i valori delle proprietà nel file di configurazione prima di eseguire gli strumenti. Per alcuni degli strumenti della riga di comando, è possibile impostare i valori per alcune opzioni tramite la riga di comando o il file di configurazione. In questi casi, i valori impostati tramite la riga di comando hanno la precedenza su qualsiasi valore nel file di configurazione.

## Installazione degli strumenti della riga di comando {#installing-the-command-line-tools}

È possibile copiare i file necessari dalla directory [!DNL \Reference Implementation\Command Line Tools] del DVD, che contiene il file di configurazione [!DNL flashaccesstools.properties] predefinito, e da una directory [!DNL libs] che contiene i file JAR per gli strumenti.

La directory [!DNL samples] contiene diversi file di origine Java di esempio che mostrano come utilizzare le API SDK di Adobe Access. Per generare ed eseguire gli esempi, utilizza lo script [!DNL build-samples.xml] Ant .