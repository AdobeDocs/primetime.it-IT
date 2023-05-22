---
title: Configurare Tomcat
description: Configurare Tomcat
copied-description: true
exl-id: 766b66dd-6070-4b0d-a860-a426fca05e56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Configurare Tomcat{#configure-tomcat}

Nel server di personalizzazione, modificare la proprietà Tomcat [!DNL conf/server.xml] per includere informazioni aggiuntive nel registro di accesso. Puoi utilizzare queste informazioni a scopo di reporting.

1. Individua la configurazione per `AccessLogValve` in [!DNL server.xml] e modificate la serie come mostrato di seguito:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registrerà il valore di `x-forwarded-for` intestazione. Se utilizzi un proxy inverso Apache per inoltrare le richieste al server Tomcat, questa intestazione conterrà l’indirizzo IP del client originale, mentre `%h` registra l’indirizzo IP del server Apache. `%{request-id}r` registrerà l’identificatore della richiesta, che corrisponde all’ID della richiesta contenuto nel registro dell’applicazione di Individualizzazione.

1. Modifica [!DNL conf/server.xml] e imposta `unpackwars` su false.

   Per entrambi i server di personalizzazione e generazione di chiavi, è consigliabile modificare [!DNL conf/server.xml] e imposta `unpackwars` proprietà a `false`. In caso contrario, quando si aggiornano i file WAR, potrebbe essere necessario eliminare anche le cartelle WAR non imballate.

>[!NOTE]
>
>I futuri client DRM richiederanno l’attivazione e la configurazione del filtro CORS (Cross-Origin Resource Sharing) disponibile per Tomcat. Attualmente, nessun client DRM dispone di questo requisito.
