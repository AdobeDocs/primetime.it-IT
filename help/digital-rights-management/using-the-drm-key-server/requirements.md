---
seo-title: Requisiti per l'utilizzo del server chiavi DRM Primetime
title: Requisiti per l'utilizzo del server chiavi DRM Primetime
uuid: 769f9e10-7a3e-4a38-b30d-18181b666bb4
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Introduzione {#introduction}

Primetime DRM Key Server è un server chiavi multi-tenant per la distribuzione remota di iOS e/o chiavi Xbox 360. Se in un criterio per iOS è abilitata la consegna delle chiavi remote, per abilitare la riproduzione del contenuto sui client iOS è necessario distribuire un server chiavi DRM Primetime. Server chiavi DRM Primetime è sempre richiesto per Xbox 360.

## Requisiti per l&#39;utilizzo del server chiavi DRM Primetime {#requirements-for-using-primetime-drm-key-server}

I requisiti minimi per l&#39;utilizzo del server chiavi DRM di Primetime sono:

* [Java JRE 1.6 ](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o versione successiva. (Per utilizzare HSM su Windows a 64 bit, è richiesto JRE 8)

   >[!NOTE]
   >
   >PKCS11 a 64 bit ora è supportato in OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131) e  Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenziali emesse dal Adobe 
* Credenziali emesse da Microsoft (per client Xbox 360)