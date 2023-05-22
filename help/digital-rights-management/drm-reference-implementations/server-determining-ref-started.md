---
title: Verificare che il server licenze sia stato avviato correttamente
description: Verificare che il server licenze sia stato avviato correttamente
copied-description: true
exl-id: 05995a75-9468-4237-9091-a07606297772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Verificare che il server licenze sia stato avviato correttamente {#check-whether-the-license-server-started-properly}

Esistono diversi modi per determinare se il server licenze di implementazione di riferimento è stato avviato correttamente. Un metodo consiste nel controllare [!DNL catalina.log] ma questo potrebbe non essere sufficiente, in quanto il server licenze registra nei propri file di registro.
1. Controlla il tuo [!DNL AdobeFlashAccess.log] file.

   In questo punto il server licenze di implementazione di riferimento scrive le informazioni di registro. La posizione di questo file di registro è indicata dal [!DNL log4j.xml] e possono essere modificati in modo da puntare a qualsiasi posizione. Per impostazione predefinita, il file di registro viene copiato nella directory di lavoro in cui si esegue `catalina` Sceneggiatura Tomcat.
1. Andare all&#39;URL seguente e verificare che venga visualizzato il testo &quot;License Server is setup correct&quot; (Il server licenze è configurato correttamente):
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
