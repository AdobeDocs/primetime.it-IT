---
title: Installare Tomcat
description: Installare Tomcat
copied-description: true
exl-id: aed8fc1c-0d75-47ca-bbd4-c0934a66e284
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Installare Tomcat {#install-tomcat}

È necessario installare Tomcat su entrambi i server.
1. Installare Tomcat da [!DNL \Third Party\Tomcat\6.0.18\] sul DVD di installazione.

   >[!NOTE]
   >
   >Verificare che Tomcat sia installato in una posizione in cui non siano presenti spazi nel percorso. È possibile immettere `C:\Program Files\Tomcat`, ma non `C:\Tomcat\`.

1. Per avviare Tomcat, immetti `TomcatInstallDir>\bin\catalina.bat run`.
1. Per verificare l’installazione, vai alla pagina di destinazione Tomcat immettendo `https://<Hostname>:8080/`.
1. Creare un `crossdomain.xml` e posizionare il file nel `<TomcatInstallDir>\webapps\ROOT\` directory.

   È inoltre possibile copiare un file da `https://drmtest2.adobe.com/crossdomain.xml` directory.
