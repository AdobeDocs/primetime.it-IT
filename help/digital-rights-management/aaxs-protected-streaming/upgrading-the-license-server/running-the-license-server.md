---
description: Per aggiornare un server che esegue Adobe Access Server per lo streaming protetto, sostituire il file flashaccessserver.war distribuito sul server dell'applicazione con il file incluso con l'accesso Adobe più recente. Se desideri utilizzare le nuove opzioni di configurazione descritte in precedenza, aggiorna il file flashaccess-tenant.xml del server. È inoltre necessario aggiornare jsafe.dll o libjsafe.so alla versione inclusa con l'ultimo accesso Adobe.
title: Esecuzione del Adobe Access Server per lo streaming protetto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Esecuzione di Adobe Access Server per lo streaming protetto{#running-the-adobe-access-server-for-protected-streaming}

Per aggiornare un server che esegue Adobe Access Server per lo streaming protetto, sostituire il file flashaccessserver.war distribuito sul server dell&#39;applicazione con il file incluso con l&#39;accesso Adobe più recente. Se desideri utilizzare le nuove opzioni di configurazione descritte in precedenza, aggiorna il file flashaccess-tenant.xml del server. È inoltre necessario aggiornare jsafe.dll o libjsafe.so alla versione inclusa con l&#39;ultimo accesso Adobe.

Prima di eseguire Adobe Access Server per lo streaming protetto, Adobe consiglia di verificare che i file di configurazione siano validi utilizzando le utility fornite con il server licenze. Per ulteriori dettagli, vedere &quot;[Convalida della configurazione](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Per avviare Tomcat e il server licenze, esegui &quot;catalina.bat start&quot; o &quot;catalina.sh start&quot; dalla directory bin di Tomcat.

Dopo aver avviato il server, verifica che sia configurato correttamente aprendo *https:// license-server-host:port/flashaccessserver/tenant-name/flashaccess/license/v1* in una finestra del browser. Se la configurazione del tenant è stata caricata correttamente, viene visualizzato un messaggio di conferma.
