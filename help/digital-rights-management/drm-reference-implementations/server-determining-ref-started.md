---
title: Verificare se il server licenze è stato avviato correttamente
description: Verificare se il server licenze è stato avviato correttamente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Verifica se il server licenze è stato avviato correttamente {#check-whether-the-license-server-started-properly}

Esistono diversi modi per determinare se il server delle licenze di implementazione di riferimento è stato avviato correttamente. Un modo è quello di controllare i registri [!DNL catalina.log], ma questo potrebbe non essere sufficiente, in quanto il server di licenze accede ai propri file di registro.
1. Controlla il tuo file [!DNL AdobeFlashAccess.log].

   Qui è dove il server delle licenze di implementazione di riferimento scrive le informazioni di registro. La posizione di questo file di registro è indicata dal file [!DNL log4j.xml] e può essere modificata in modo che punti a qualsiasi posizione. Per impostazione predefinita, il file di registro viene copiato nella directory di lavoro in cui viene eseguito lo script `catalina` Tomcat.
1. Vai al seguente URL e verifica che venga visualizzato il testo &quot;License Server is setup right&quot; (Server licenze configurato correttamente):
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
