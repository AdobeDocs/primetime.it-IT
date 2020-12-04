---
seo-title: Configura Tomcat
title: Configura Tomcat
uuid: 5f23aa33-29d7-4b41-87a4-59dc5b433de4
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Configura Tomcat{#configure-tomcat}

Nel server di Individualizzazione, modificate il file [!DNL conf/server.xml] di Tomcat per includere ulteriori informazioni nel registro di accesso. Potete utilizzare queste informazioni a scopo di reporting.

1. Individuare la configurazione della `AccessLogValve` in [!DNL server.xml] e modificare il pattern come illustrato di seguito:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registra il valore dell&#39; `x-forwarded-for` intestazione. Se utilizzate un proxy inverso Apache per inoltrare le richieste al server Tomcat, questa intestazione conterrà l&#39;indirizzo IP del client originale, mentre `%h` registrerà l&#39;indirizzo IP del server Apache. `%{request-id}r` registrerà l&#39;identificatore della richiesta, che corrisponde all&#39;ID della richiesta contenuto nel registro dell&#39;applicazione Individualizzazione.

1. Modificare [!DNL conf/server.xml] e impostare la proprietà `unpackwars` su false.

   Sia per i server Individualization che per i server Key Generation, è consigliabile modificare [!DNL conf/server.xml] e impostare la proprietà `unpackwars` su `false`. In caso contrario, quando si aggiornano le WAR, potrebbe essere necessario pulire anche le cartelle WAR non imballate.

>[!NOTE]
>
>I futuri client DRM dovranno abilitare e configurare il filtro CORS (Cross-Origin Resource Sharing) disponibile per Tomcat. Al momento, nessun client DRM ha questo requisito.

