---
title: Requisiti per l'utilizzo del server chiavi DRM di Primetime
description: Requisiti per l'utilizzo del server chiavi DRM di Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Introduzione {#introduction}

Server chiavi DRM di Primetime è un server chiavi multi-tenant per iOS remoto e / o la consegna chiavi Xbox 360. Se in un criterio per iOS è abilitata l’opzione Consegna chiavi remota , è necessario distribuire un server chiavi DRM di Primetime per abilitare la riproduzione di contenuti sui client iOS. Il server chiavi DRM di Primetime è sempre necessario per Xbox 360.

## Requisiti per l&#39;utilizzo del server chiavi DRM di Primetime {#requirements-for-using-primetime-drm-key-server}

I requisiti minimi per l&#39;utilizzo del server chiavi DRM di Primetime sono i seguenti:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o versione successiva. (Per utilizzare HSM su Windows a 64 bit, è richiesto JRE 8)

   >[!NOTE]
   >
   >OpenJDK 8 supporta ora PKCS11 a 64 bit: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131) e Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Crediti emessi dall&#39;Adobe
* Credenziali rilasciate da Microsoft (per client Xbox 360)