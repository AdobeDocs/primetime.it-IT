---
title: Requisiti per l'utilizzo di Primetime DRM Key Server
description: Requisiti per l'utilizzo di Primetime DRM Key Server
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Introduzione {#introduction}

Primetime DRM Key Server è un Key Server multi-tenant per la distribuzione remota di iOS e/o Xbox 360. Se in un criterio per iOS è abilitata l’opzione Consegna chiavi remote, è necessario distribuire un server chiavi DRM Primetime per abilitare la riproduzione dei contenuti sui client iOS. Primetime DRM Key Server è sempre richiesto per Xbox 360.

## Requisiti per l&#39;utilizzo di Primetime DRM Key Server {#requirements-for-using-primetime-drm-key-server}

I requisiti minimi per l&#39;utilizzo di Primetime DRM Key Server sono i seguenti:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o più tardi. (per utilizzare HSM su Windows a 64 bit, è necessario JRE 8)

  >[!NOTE]
  >
  >Il PKCS11 a 64 bit è ora supportato in OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131), e ORACLE
* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenziali emesse da Adobe
* Credenziali emesse da Microsoft (per client Xbox 360)
