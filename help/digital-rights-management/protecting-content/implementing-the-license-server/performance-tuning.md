---
seo-title: Ottimizzazione delle prestazioni
title: Ottimizzazione delle prestazioni
uuid: db8889c7-ecf5-4551-a6fc-1d3ab992b9ff
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Ottimizzazione delle prestazioni{#performance-tuning}

Utilizzate i seguenti suggerimenti per migliorare le prestazioni:

* L&#39;utilizzo di un HSM di rete può risultare notevolmente più lento rispetto all&#39;utilizzo di un HSM connesso direttamente.
* Per migliorare le prestazioni, puoi facoltativamente abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche della piattaforma che si trovano nella cartella [!DNL thirdparty/cryptoj] dell&#39;SDK. Per abilitare il supporto nativo, aggiungete al percorso la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux).

   >[!NOTE]
   >
   >Se si eseguono più applicazioni Web nella stessa istanza Tomcat e si trovano nel percorso `jsafe.dll`, solo la prima applicazione Web caricata sarà in grado di caricare la libreria `jsafe.dll`. Pertanto, solo la prima applicazione Web ottiene il vantaggio del supporto nativo. In tali casi, per migliorare le prestazioni di tutte le applicazioni Web, posizionare `cryptoj.jar`all&#39;esterno del file WAR. Ad esempio, nella directory `<tomcat_installation_folder>/lib`.

* Un sistema operativo a 64 bit, come la versione a 64 bit di Red Hat® o Windows, offre prestazioni migliori rispetto a un sistema operativo a 32 bit.

## Generazione di numeri casuali (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

In determinate condizioni, gli ambienti Linux possono interrompersi durante le operazioni relative a Primetime DRM che richiedono la generazione casuale di numeri, tra cui:

* Avvio del server di licenze Adobe Primetime DRM 
* Generazione dei criteri tramite l&#39;utilità [!DNL AdobePolicyManager]
* Creazione di pacchetti di contenuto protetto da DRM con  Adobe Media Server o con Primetime OfflinePackager

I ritardi durante queste operazioni sono spesso il risultato di un pool entropico basso sul server Linux.

In Linux, i numeri casuali vengono generati dal pool di entropia dell&#39;ambiente server. Il pool entropico viene normalmente mantenuto ricevendo interruzioni hardware dal kernel Linux. Se un server è isolato e non riceve un input regolare da risorse HW (ad esempio un mouse o una tastiera), le attese per riempire il pool di entropia possono essere estese. In questo scenario, le operazioni in attesa dei dati da [!DNL /dev/random] potrebbero interrompersi.

È possibile utilizzare generatori di numeri casuali hardware sui server Linux per garantire che venga generata un&#39;entropia sufficiente. Tuttavia, se i generatori di numeri casuali hardware non sono disponibili in uno scenario di distribuzione specifico, potete utilizzare soluzioni basate su software per aumentare la frequenza di aggiornamento del pool di entropia. Una di tali soluzioni software su Linux è [!DNL haveged] (il demone di raccolta e espansione dell&#39;Entropia Volatile HArdware).

## Determinazione dell&#39;Entropia disponibile {#section_686B311FE6144566B6939E9F20915ADC}

Per verificare il numero di bit disponibili nel pool di entropia di un determinato server durante un ritardo imprevisto, eseguire il comando seguente:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Un sistema Linux sano con un sacco di entropia disponibile tornerà vicino al pieno 4.096 bit di entropia. Se il valore restituito è inferiore a 200, l&#39;entropia del sistema è molto bassa.
