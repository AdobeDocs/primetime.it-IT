---
title: Requisiti per l'utilizzo di Primetime DRM Key Server
description: Requisiti per l'utilizzo di Primetime DRM Key Server
copied-description: true
exl-id: a5c0db05-15a1-45b0-abb9-11f857f5e34c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Introduzione {#introduction}

Primetime DRM Key Server è un Key Server multi-tenant per la distribuzione remota di iOS e/o Xbox 360. Se in un criterio per iOS è abilitata l’opzione Consegna chiavi remote, è necessario distribuire un server chiavi DRM Primetime per abilitare la riproduzione dei contenuti sui client iOS. Primetime DRM Key Server è sempre richiesto per Xbox 360.

## Requisiti per l&#39;utilizzo di Primetime DRM Key Server {#requirements-for-using-primetime-drm-key-server}

I requisiti minimi per l&#39;utilizzo di Primetime DRM Key Server sono i seguenti:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o più tardi. (per utilizzare HSM su Windows a 64 bit, è necessario JRE 8)

   >[!NOTE]
   >
   >Il PKCS11 a 64 bit è ora supportato in OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131), e Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenziali emesse da Adobe
* Credenziali emesse da Microsoft (per client Xbox 360)
