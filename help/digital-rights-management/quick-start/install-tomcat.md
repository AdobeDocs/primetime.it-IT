---
seo-title: Installa Tomcat
title: Installa Tomcat
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Installazione di Tomcat {#install-tomcat}

È necessario installare Tomcat su entrambi i server.
1. Installare Tomcat dalla directory  [!DNL \Third Party\Tomcat\6.0.18\] del DVD di installazione.

   >[!NOTE]
   >
   >Assicurarsi che Tomcat sia installato in una posizione in cui non ci sono spazi nel percorso. È possibile immettere `C:\Program Files\Tomcat`, ma non `C:\Tomcat\`.

1. Per avviare Tomcat, immettere `TomcatInstallDir>\bin\catalina.bat run`.
1. Per verificare l&#39;installazione, andate alla pagina di destinazione Tomcat immettendo `https://<Hostname>:8080/`.
1. Create un file `crossdomain.xml` e inserite il file nella directory `<TomcatInstallDir>\webapps\ROOT\`.

   È inoltre possibile copiare un file dalla directory `https://drmtest2.adobe.com/crossdomain.xml`.
