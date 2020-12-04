---
description: Per aggiornare un server che esegue Adobe Access Server per lo streaming protetto, sostituire il file flashaccessserver.war distribuito sul server dell'applicazione con il file incluso con l'accesso al Adobe  più recente. Se desiderate utilizzare le nuove opzioni di configurazione descritte in precedenza, aggiornate il file flashaccess-tenant.xml del server. È inoltre necessario aggiornare jsafe.dll o libjsafe.so alla versione inclusa con l'ultimo accesso  Adobe.
seo-description: Per aggiornare un server che esegue Adobe Access Server per lo streaming protetto, sostituire il file flashaccessserver.war distribuito sul server dell'applicazione con il file incluso con l'accesso al Adobe  più recente. Se desiderate utilizzare le nuove opzioni di configurazione descritte in precedenza, aggiornate il file flashaccess-tenant.xml del server. È inoltre necessario aggiornare jsafe.dll o libjsafe.so alla versione inclusa con l'ultimo accesso  Adobe.
seo-title: Esecuzione di Adobe Access Server per lo streaming protetto
title: Esecuzione di Adobe Access Server per lo streaming protetto
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Esecuzione di Adobe Access Server per lo streaming protetto{#running-the-adobe-access-server-for-protected-streaming}

Per aggiornare un server che esegue Adobe Access Server per lo streaming protetto, sostituire il file flashaccessserver.war distribuito sul server dell&#39;applicazione con il file incluso con l&#39;accesso al Adobe  più recente. Se desiderate utilizzare le nuove opzioni di configurazione descritte in precedenza, aggiornate il file flashaccess-tenant.xml del server. È inoltre necessario aggiornare jsafe.dll o libjsafe.so alla versione inclusa con l&#39;ultimo accesso  Adobe.

Prima di eseguire Adobe Access Server per lo streaming protetto,  Adobe consiglia di verificare la validità dei file di configurazione utilizzando le utility fornite con il server licenze. Per ulteriori dettagli, vedere &quot;[Convalida della configurazione](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Per avviare Tomcat e il server licenze, eseguire &quot;catalina.bat start&quot; o &quot;catalina.sh start&quot; dalla directory bin di Tomcat.

Dopo l&#39;avvio del server, verificate che sia configurato correttamente aprendo *https:// license-server-host:port/flashaccessserver/tenant-name/flashaccess/license/v1* in una finestra del browser. Se la configurazione del tenant è stata caricata correttamente, viene visualizzato un messaggio di conferma.
