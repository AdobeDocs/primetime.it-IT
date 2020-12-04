---
description: 'null'
seo-description: 'null'
seo-title: Verificare se il server licenze è stato avviato correttamente
title: Verificare se il server licenze è stato avviato correttamente
uuid: a6a034c9-b3c4-4e26-b901-d2c132c00c52
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Verificare se il server licenze è stato avviato correttamente {#check-whether-the-license-server-started-properly}

Esistono diversi modi per determinare se il server delle licenze di implementazione di riferimento è stato avviato correttamente. Un modo è quello di controllare i [!DNL catalina.log] registri, ma questo potrebbe non essere sufficiente, in quanto il server licenze accede ai propri file di registro.
1. Controllare il file [!DNL AdobeFlashAccess.log].

   In questa area vengono scritte le informazioni di registro nel server delle licenze di implementazione di riferimento. Il percorso di questo file di registro è indicato dal file [!DNL log4j.xml] e può essere modificato per puntare a qualsiasi percorso. Per impostazione predefinita, il file di registro viene copiato nella directory di lavoro in cui viene eseguito lo script `catalina` Tomcat.
1. Accedete al seguente URL e verificate che sia visualizzato il testo &quot;License Server is setup correct&quot;:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
