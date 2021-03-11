---
description: È possibile impostare il lettore per leggere le statistiche di riproduzione e dispositivo dal QoSProvider ogni volta che necessario.
title: Visualizzazione delle statistiche di riproduzione e dispositivo QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Visualizzazione delle statistiche relative a riproduzione e dispositivo QoS {#display-qos-playback-and-device-statistics}

È possibile impostare il lettore per leggere le statistiche di riproduzione e dispositivo dal QoSProvider ogni volta che necessario.

La classe `QoSProvider` fornisce diverse statistiche, tra cui il frame rate, il bit rate del profilo, il tempo totale trascorso nel buffering, il numero di tentativi di buffering, il tempo necessario per ottenere il primo byte dal primo frammento video, il tempo necessario per eseguire il rendering del primo fotogramma, la lunghezza attualmente bufferizzata e il tempo di buffer.

L&#39;implementazione di riferimento fornisce una classe `QoSManager` in cui puoi abilitare la visualizzazione della sovrapposizione QoS. È inoltre possibile abilitare la visibilità QoS nell&#39;interfaccia utente Impostazioni:

![](assets/qos-configuration.jpg)

Il `QoSManager` tiene traccia delle statistiche di QoS ottenendo informazioni sul dispositivo, allegando al lettore multimediale e aggiornando con le ultime informazioni di QoS.

**Attivare o disattivare la generazione di rapporti sulle statistiche QoS**

1. Crea un QosManager o abilita il reporting QoS utilizzando ManagerFactory.

   * Per creare un QosManager:
      * Questa applicazione deve utilizzare la funzione del flusso di lavoro pubblicitario

   QoSManager qosManager = nuovo QosManagerOn();

   * Per utilizzare un ManagerFactory per abilitare la visualizzazione delle statistiche QoS:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >La modifica del valore booleano in `false` disattiva la generazione di rapporti QoS.

2. Aggiungi listener di eventi:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Crea il provider QoS e collegalo al contesto dell&#39;attività del lettore:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Quando l&#39;attività del lettore verrà distrutta, assicurati di chiamare [qosManager.uninstallQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) per pulire il provider QOS staccandolo dal lettore multimediale.

**Documentazione API correlata**

* [Classe QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Classe QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
