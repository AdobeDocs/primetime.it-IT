---
title: Installa Tomcat
description: Installa Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Installa Tomcat {#install-tomcat}

Devi installare Tomcat su entrambi i server.
1. Installare Tomcat dalla directory [!DNL \Third Party\Tomcat\6.0.18\] del DVD di installazione.

   >[!NOTE]
   >
   >Assicurati che Tomcat sia installato in una posizione in cui non ci sono spazi nel percorso. È possibile immettere `C:\Program Files\Tomcat`, ma non `C:\Tomcat\`.

1. Per avviare Tomcat, immetti `TomcatInstallDir>\bin\catalina.bat run`.
1. Per verificare l’installazione, vai alla pagina di destinazione Tomcat immettendo `https://<Hostname>:8080/`.
1. Crea un file `crossdomain.xml` e inserisci il file nella directory `<TomcatInstallDir>\webapps\ROOT\` .

   Puoi anche copiare un file dalla directory `https://drmtest2.adobe.com/crossdomain.xml`.
