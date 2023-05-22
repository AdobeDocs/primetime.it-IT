---
description: È possibile impostare il lettore in modo che legga le statistiche della riproduzione e del dispositivo da QoSProvider ogni volta che è necessario.
title: Visualizzare le statistiche della riproduzione QoS e del dispositivo
exl-id: 369b6e9a-70a2-4f62-a1bf-f69030c5d6c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Visualizzare le statistiche della riproduzione QoS e del dispositivo {#display-qos-playback-and-device-statistics}

È possibile impostare il lettore in modo che legga le statistiche della riproduzione e del dispositivo da QoSProvider ogni volta che è necessario.

Il `QoSProvider` class fornisce varie statistiche, tra cui il frame rate, il bit rate del profilo, il tempo totale trascorso nel buffering, il numero di tentativi di buffering, il tempo necessario per ottenere il primo byte dal primo frammento video, il tempo necessario per il rendering del primo fotogramma, la lunghezza attualmente inserita nel buffering e il tempo del buffer.

L’implementazione di riferimento fornisce `QoSManager` in cui è possibile abilitare la visualizzazione della sovrapposizione QoS. Puoi anche abilitare la visibilità QoS nell’interfaccia utente Impostazioni:

![](assets/qos-configuration.jpg)

Il `QoSManager` tiene traccia delle statistiche QoS ottenendo informazioni sul dispositivo, collegandosi al lettore multimediale e aggiornando le informazioni QoS più recenti.

**Abilita o disabilita il reporting delle statistiche QoS**

1. Crea un QosManager o abilita la generazione di rapporti QoS utilizzando ManagerFactory.

   * Per creare un QosManager:
      * Questa applicazione deve utilizzare la funzione per flussi di lavoro pubblicitari

   QoSManager qosManager = nuovo QosManagerOn();

   * Per utilizzare un oggetto ManagerFactory per abilitare la visualizzazione delle statistiche QoS:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >Modifica del valore booleano in `false` disabilita il reporting QoS.

2. Aggiungi listener di eventi:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Crea il provider QoS e allegalo al contesto di attività del lettore:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Quando l’attività del lettore verrà distrutta, assicurati di chiamare [qosManager.diesQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) per pulire il provider QOS scollegandolo dal lettore multimediale.

**Documentazione API correlata**

* [Class QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Class QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
