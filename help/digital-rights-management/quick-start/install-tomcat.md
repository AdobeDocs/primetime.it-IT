---
seo-title: Installa Tomcat
title: Installa Tomcat
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Installa Tomcat {#install-tomcat}

È necessario installare Tomcat su entrambi i server.
1. Installate Tomcat dalla directory [!DNL \Third Party\Tomcat\6.0.18\] sul DVD di installazione.

   >[!NOTE]
   >
   >Assicurarsi che Tomcat sia installato in una posizione in cui non ci sono spazi nel percorso. Potete entrare `C:\Program Files\Tomcat`, ma non `C:\Tomcat\`.

1. Per iniziare Tomcat, entra `TomcatInstallDir>\bin\catalina.bat run`.
1. Per verificare l&#39;installazione, accedete alla pagina di destinazione Tomcat `https://<Hostname>:8080/`.
1. Create un `crossdomain.xml` file e inseritelo nella `<TomcatInstallDir>\webapps\ROOT\` directory.

   Potete anche copiare un file dalla `https://drmtest2.adobe.com/crossdomain.xml` directory.
