---
title: Configura Tomcat
description: Configura Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Configura Tomcat{#configure-tomcat}

Sul server Individualization, modifica il file [!DNL conf/server.xml] di Tomcat per includere informazioni aggiuntive nel registro di accesso. Puoi utilizzare queste informazioni a scopo di reporting.

1. Individua la configurazione per `AccessLogValve` in [!DNL server.xml] e modifica il pattern come mostrato di seguito:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registra il valore dell&#39; `x-forwarded-for` intestazione. Se utilizzi un proxy inverso Apache per inoltrare le richieste al server Tomcat, questa intestazione conterrà l’indirizzo IP del client originale, mentre `%h` registra l’indirizzo IP del server Apache. `%{request-id}r` registra l’identificatore della richiesta, corrispondente all’ID della richiesta contenuto nel registro dell’applicazione Individualization.

1. Modifica [!DNL conf/server.xml] e imposta la proprietà `unpackwars` su false.

   Per i server Individualization e Key Generation , è consigliabile modificare [!DNL conf/server.xml] e impostare la proprietà `unpackwars` su `false`. In caso contrario, quando si aggiornano le WAR, potrebbe essere necessario pulire anche le cartelle WAR scompattate.

>[!NOTE]
>
>I futuri client DRM richiederanno di abilitare e configurare il filtro CORS (Cross-Origin Resource Sharing) disponibile per Tomcat. Attualmente, nessun cliente DRM ha questo requisito.

