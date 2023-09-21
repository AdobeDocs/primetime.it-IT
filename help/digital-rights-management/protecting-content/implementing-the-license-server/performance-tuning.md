---
title: Ottimizzazione delle prestazioni
description: Ottimizzazione delle prestazioni
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Ottimizzazione delle prestazioni{#performance-tuning}

Utilizza i seguenti suggerimenti per migliorare le prestazioni:

* L&#39;utilizzo di un HSM di rete può essere notevolmente più lento rispetto all&#39;utilizzo di un HSM a connessione diretta.
* Per migliorare le prestazioni, è possibile abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche della piattaforma che si trovano in [!DNL thirdparty/cryptoj] cartella dell’SDK. Per abilitare il supporto nativo, aggiungi la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux) al percorso.

  >[!NOTE]
  >
  >Se esegui più applicazioni web nella stessa istanza Tomcat e disponi di `jsafe.dll` sul percorso, solo la prima applicazione web che carica è in grado di caricare `jsafe.dll` libreria. Pertanto, solo la prima applicazione web ottiene il vantaggio del supporto nativo. In questi casi, per migliorare le prestazioni di tutte le applicazioni web, inserisci `cryptoj.jar`all&#39;esterno del file WAR. Ad esempio, nel `<tomcat_installation_folder>/lib` directory.

* Un sistema operativo a 64 bit, come la versione a 64 bit di Red Hat® o Windows, offre prestazioni molto migliori rispetto a un sistema operativo a 32 bit.

## Generazione di numeri casuali (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

In determinate condizioni gli ambienti Linux possono essere messi in pausa durante l&#39;esecuzione di operazioni Primetime relative a DRM che richiedono la generazione di numeri casuali, tra cui:

* Avvio del server licenze Adobe Primetime DRM
* Generazione di criteri tramite [!DNL AdobePolicyManager] utilità
* Creazione di pacchetti di contenuti protetti da DRM con Adobe Media Server o OfflinePackager di Primetime

I ritardi durante queste operazioni sono spesso il risultato di un pool entropico basso sul server Linux.

Su Linux, i numeri casuali vengono generati dal pool di entropia dell&#39;ambiente server. Il pool di entropia viene normalmente mantenuto ricevendo interrupt hardware dal kernel Linux. Se un server è isolato e non riceve input regolari dalle risorse hardware (come un mouse o una tastiera), l&#39;attesa di ricaricare il pool di entropia può essere estesa. In questo scenario, le operazioni in attesa di dati da [!DNL /dev/random] può sospendere.

È possibile utilizzare generatori di numeri casuali hardware sui server Linux per garantire che venga generata un&#39;entropia sufficiente. Tuttavia, se i generatori di numeri casuali hardware non sono disponibili in un determinato scenario di distribuzione, è possibile utilizzare soluzioni basate su software per aumentare la frequenza di aggiornamento del pool di entropia. Una di queste soluzioni software su Linux è [!DNL haveged] (Daemon di espansione e raccolta di entropia volatile HArdware).

## Determinazione dell’entropia disponibile {#section_686B311FE6144566B6939E9F20915ADC}

Per verificare il numero di bit disponibili nel pool di entropia di un determinato server durante un ritardo imprevisto, eseguire il comando seguente:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Un sistema Linux sano con molta entropia disponibile tornerà vicino ai 4.096 bit completi di entropia. Se il valore restituito è inferiore a 200, l&#39;entropia del sistema è molto bassa.
