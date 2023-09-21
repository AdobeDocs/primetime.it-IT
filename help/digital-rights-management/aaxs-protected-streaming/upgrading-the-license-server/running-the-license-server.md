---
description: Per aggiornare un server che esegue Adobe Access Server for Protected Streaming, sostituire il file flashaccessserver.war distribuito sul server applicazioni con il file incluso con l'Adobe di accesso più recente. Se si desidera utilizzare le nuove opzioni di configurazione descritte in precedenza, aggiornare flashaccess-tenant.xml del server. È inoltre necessario aggiornare jsafe.dll o libjsafe.so alla versione inclusa nell’Adobe più recente.
title: Esecuzione di Adobe Access Server per lo streaming protetto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Esecuzione di Adobe Access Server per lo streaming protetto{#running-the-adobe-access-server-for-protected-streaming}

Per aggiornare un server che esegue Adobe Access Server for Protected Streaming, sostituire il file flashaccessserver.war distribuito sul server applicazioni con il file incluso con l&#39;Adobe di accesso più recente. Se si desidera utilizzare le nuove opzioni di configurazione descritte in precedenza, aggiornare flashaccess-tenant.xml del server. È inoltre necessario aggiornare jsafe.dll o libjsafe.so alla versione inclusa nell’Adobe più recente.

Prima di eseguire Adobe Access Server for Protected Streaming, l&#39;Adobe consiglia di verificare che i file di configurazione siano validi utilizzando le utilità fornite con il server licenze. Per ulteriori dettagli, consulta &quot;[Convalida configurazione](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Per avviare Tomcat e il server licenze, eseguire &quot;catalina.bat start&quot; o &quot;catalina.sh start&quot; dalla directory bin di Tomcat.

Dopo l&#39;avvio del server, verificare che sia configurato correttamente aprendo *https:// license-server-host:port/flashaccessserver/tenant-name/flashaccess/license/v1* in una finestra del browser. Se la configurazione del tenant è stata caricata correttamente, viene visualizzato un messaggio di conferma.
