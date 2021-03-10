---
title: Ottimizzazione delle prestazioni
description: Ottimizzazione delle prestazioni
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Ottimizzazione delle prestazioni{#performance-tuning}

Utilizza i seguenti suggerimenti per migliorare le prestazioni:

* L&#39;utilizzo di un HSM di rete può essere notevolmente più lento rispetto all&#39;utilizzo di un HSM collegato direttamente.
* Per migliorare le prestazioni, puoi facoltativamente abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche della piattaforma che si trovano nella cartella [!DNL thirdparty/cryptoj] dell’SDK. Per abilitare il supporto nativo, aggiungi la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux) al percorso.

   >[!NOTE]
   >
   >Se esegui più applicazioni web nella stessa istanza Tomcat e disponi di `jsafe.dll` sul percorso, solo la prima applicazione web che viene caricata sarà in grado di caricare la libreria `jsafe.dll`. Pertanto, solo la prima applicazione web ottiene il vantaggio del supporto nativo. In questi casi, per migliorare le prestazioni di tutte le applicazioni web, posizionare `cryptoj.jar`al di fuori del file WAR. Ad esempio, nella directory `<tomcat_installation_folder>/lib`.

* Un sistema operativo a 64 bit, come la versione a 64 bit di Red Hat® o Windows, offre prestazioni molto migliori rispetto a un sistema operativo a 32 bit.

## Generazione di numeri casuali (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

In determinate condizioni gli ambienti Linux possono fermarsi quando si eseguono operazioni relative a DRM di Primetime che richiedono la generazione casuale di numeri, tra cui:

* Avvio del server licenze Adobe Primetime DRM
* Generazione dei criteri tramite l&#39;utility [!DNL AdobePolicyManager]
* Confezione di contenuti protetti da DRM con Adobe Medium Server o Primetime OfflinePackager

I ritardi durante queste operazioni sono spesso il risultato di un pool entropico basso sul server Linux.

Su Linux, i numeri casuali vengono generati dal pool di entropia dell&#39;ambiente server. Il pool entropico viene normalmente mantenuto ricevendo interruzioni hardware dal kernel Linux. Se un server è isolato e non riceve un input regolare da risorse HW (come un mouse o una tastiera), l&#39;attesa di ricaricare il pool entropia può essere estesa. In questo scenario, le operazioni in attesa dei dati da [!DNL /dev/random] potrebbero essere in pausa.

È possibile utilizzare generatori di numeri casuali hardware sui server Linux per garantire che venga generata un&#39;entropia sufficiente. Tuttavia, se i generatori di numeri casuali hardware non sono disponibili in un dato scenario di distribuzione, è possibile utilizzare soluzioni basate su software per aumentare la frequenza di aggiornamento del pool entropico. Una di tali soluzioni software su Linux è [!DNL haveged] (il daemon di raccolta e espansione dell&#39;entropia volatile HArdware).

## Determinazione dell&#39;Entropia disponibile {#section_686B311FE6144566B6939E9F20915ADC}

Per verificare il numero di bit disponibili nel pool di entropia di un determinato server durante un ritardo imprevisto, eseguire il comando seguente:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Un sistema Linux sano con un sacco di entropia disponibile tornerà vicino al pieno 4.096 bit di entropia. Se il valore restituito è inferiore a 200, l&#39;entropia del sistema è molto bassa.
