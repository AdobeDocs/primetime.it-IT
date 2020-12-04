---
description: È possibile impostare il lettore in modo che legga le statistiche relative a riproduzione e dispositivo dal QoSProvider ogni volta che necessario.
seo-description: È possibile impostare il lettore in modo che legga le statistiche relative a riproduzione e dispositivo dal QoSProvider ogni volta che necessario.
seo-title: Visualizzare le statistiche sulla riproduzione e sul dispositivo QoS
title: Visualizzare le statistiche sulla riproduzione e sul dispositivo QoS
uuid: 8fc45a2f-03d4-4fa0-979b-eb816419c4f7
translation-type: tm+mt
source-git-commit: e1c6ab1d50f9262aaf70aef34854cf293fb4f30d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Visualizza le statistiche relative a riproduzione e dispositivo QoS {#display-qos-playback-and-device-statistics}

È possibile impostare il lettore in modo che legga le statistiche relative a riproduzione e dispositivo dal QoSProvider ogni volta che necessario.

La classe `QoSProvider` fornisce diverse statistiche, tra cui il frame rate, il bit rate del profilo, il tempo totale trascorso nel buffering, il numero di tentativi di buffering, il tempo necessario per ottenere il primo byte dal primo frammento video, il tempo necessario per eseguire il rendering del primo fotogramma, la lunghezza attualmente memorizzata nel buffer e il tempo di buffer.

L&#39;implementazione di riferimento fornisce una classe `QoSManager` in cui è possibile attivare la visualizzazione della sovrapposizione QoS. Potete inoltre abilitare la visibilità QoS nell&#39;interfaccia utente Impostazioni:

![](assets/qos-configuration.jpg)

Il `QoSManager` tiene traccia delle statistiche QoS ottenendo informazioni sul dispositivo, collegandosi al lettore multimediale e aggiornandosi con le informazioni QoS più recenti.

**Attivare o disattivare la generazione di rapporti sulle statistiche di QoS**

1. Create un QosManager o abilitate il reporting QoS utilizzando ManagerFactory.

   * Per creare un QosManager:
      * Questa applicazione deve utilizzare la funzione del flusso di lavoro pubblicitario

   QoSManager qosManager = nuovo QosManagerOn();

   * Per utilizzare ManagerFactory per attivare la visualizzazione delle statistiche di QoS:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >Modificando il valore booleano in `false` viene disattivata la generazione di rapporti QoS.

2. Aggiungete i listener di eventi:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Create il provider QoS e collegatelo al contesto dell&#39;attività del lettore:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Quando l&#39;attività del lettore verrà distrutta, assicurarsi di chiamare [qosManager.distruggereQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) per ripulire il provider QOS staccandolo dal lettore multimediale.

**Documentazione API correlata**

* [Classe QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Classe QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
