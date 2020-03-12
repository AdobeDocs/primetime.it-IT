---
seo-title: Configura Tomcat
title: Configura Tomcat
uuid: 5f23aa33-29d7-4b41-87a4-59dc5b433de4
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Configura Tomcat{#configure-tomcat}

Nel server Individualization, modificate il [!DNL conf/server.xml] file Tomcat per includere informazioni aggiuntive nel registro di accesso. Potete utilizzare queste informazioni a scopo di reporting.

1. Individuare la configurazione per `AccessLogValve` in [!DNL server.xml] e modificare il pattern come mostrato di seguito:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registra il valore dell&#39; `x-forwarded-for` intestazione. Se utilizzate un proxy inverso Apache per inoltrare le richieste al server Tomcat, questa intestazione conterrà l&#39;indirizzo IP del client originale, mentre `%h` registra l&#39;indirizzo IP del server Apache. `%{request-id}r` registrerà l&#39;identificatore della richiesta, che corrisponde all&#39;ID della richiesta contenuto nel registro dell&#39;applicazione Individualizzazione.

1. Modificate [!DNL conf/server.xml] e impostate la `unpackwars` proprietà su false.

   Sia per i server di Individualizzazione che per i server di generazione delle chiavi, è consigliabile modificare [!DNL conf/server.xml] e impostare la `unpackwars` proprietà su `false`. In caso contrario, quando si aggiornano le WAR, potrebbe essere necessario pulire anche le cartelle WAR non imballate.

>[!NOTE]
>
>I futuri client DRM dovranno abilitare e configurare il filtro CORS (Cross-Origin Resource Sharing) disponibile per Tomcat. Al momento, nessun client DRM ha questo requisito.

