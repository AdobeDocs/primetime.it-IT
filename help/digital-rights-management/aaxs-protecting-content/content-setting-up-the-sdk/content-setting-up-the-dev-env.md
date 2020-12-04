---
description: Per configurare il Adobe ® Access™ per l'uso, copiate i file dal DVD. Questi file includono file JAR contenenti codice, certificati e classi di terze parti. Inoltre, richiedete un certificato da Adobe Systems Incorporated. Verranno rilasciate più credenziali utilizzate per proteggere l'integrità del contenuto, delle licenze e della comunicazione del pacchetto tra client e server.
seo-description: Per configurare il Adobe ® Access™ per l'uso, copiate i file dal DVD. Questi file includono file JAR contenenti codice, certificati e classi di terze parti. Inoltre, richiedete un certificato da Adobe Systems Incorporated. Verranno rilasciate più credenziali utilizzate per proteggere l'integrità del contenuto, delle licenze e della comunicazione del pacchetto tra client e server.
seo-title: Impostazione dell'ambiente di sviluppo
title: Impostazione dell'ambiente di sviluppo
uuid: 1f192783-9c9a-4342-909a-4881248a85ad
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Impostazione dell&#39;SDK {#setting-up-the-sdk}

Per configurare il Adobe ® Access™ per l&#39;uso, copiate i file dal DVD. Questi file includono file JAR contenenti codice, certificati e classi di terze parti. Inoltre, richiedete un certificato da Adobe Systems Incorporated. Verranno rilasciate più credenziali utilizzate per proteggere l&#39;integrità del contenuto, delle licenze e della comunicazione del pacchetto tra client e server.

L&#39;SDK per l&#39;accesso al Adobe  è disponibile in due tipi:
* Adobe Access Core SDK
* Adobe Access Professional SDK

Nella tabella seguente è riportato un confronto di base tra  SDK di accesso ai Adobi:

| Feature | Adobe Access Core SDK | Adobe Access Professional SDK |
|---|---|---|
| Funzioni di Flash Access 2.0 | Disponibile | Disponibile |
| Rotazione chiave | - | Disponibile |
| Supporto di dominio | Disponibile | Disponibile |
| Concatenamento Delle Licenze Migliorato | Disponibile | Disponibile |
| Messaggi di sincronizzazione | Disponibile | Disponibile |
| Pre-Generazione licenza | Disponibile | Disponibile |
| Licenze incorporate | Disponibile | Disponibile |

## Impostazione dell&#39;ambiente di sviluppo {#setting-up-the-development-environment}

Dal DVD, copiate i seguenti file SDK da usare nel vostro ambiente di sviluppo e nel percorso di classe Java:

* adobe-flashaccess-certs.jar (contiene  certificati radice di Adobe)
* adobe-flashaccess-sdk.jar (contiene le classi SDK per Adobe Access Core)
* adobe-flashaccess-sdk-pro.jar (contiene le classi SDK per Adobe Access Professional, richieste solo per le funzioni Professional)

Nel DVD sono necessari anche i seguenti file JAR di terze parti che si trovano nella cartella &quot;third-party&quot; dell&#39;SDK:

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discovery-0.4.jar
* commons-logging-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

Per migliorare le prestazioni, puoi facoltativamente abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche della piattaforma che si trovano nella cartella &quot;third-party/cryptoj&quot; dell’SDK. Per abilitare il supporto nativo, aggiungete al percorso la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux). Vengono fornite le versioni a 32 bit e a 64 bit di queste librerie. La versione a 64 bit deve essere utilizzata solo se si dispone di un sistema operativo a 64 bit e si esegue la versione a 64 bit di Java.

Inoltre, una parte facoltativa dell’SDK è adobe-flashaccess-lcrm.jar. Questo file è necessario solo per le funzionalità relative  compatibilità di Media Rights Management Adobe Flash (FMRMS) 1.x. Se avete distribuito in precedenza FMRMS 1.x e non desiderate creare nuovamente il pacchetto con contenuto protetto FMRMS, dovete aggiungere il supporto al server delle licenze in modo che possa gestire vecchi contenuti e client.
