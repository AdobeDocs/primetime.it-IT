---
description: Per configurare Adobe® Access™ per l'utilizzo, copiare i file dal DVD. Questi file includono file JAR contenenti codice, certificati e classi di terze parti. Inoltre, richiedi un certificato da Adobe Systems Incorporated. Verranno rilasciate più credenziali utilizzate per proteggere l'integrità del contenuto, delle licenze e della comunicazione in pacchetto tra client e server.
title: Impostazione dell'ambiente di sviluppo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Configurazione dell&#39;SDK {#setting-up-the-sdk}

Per configurare Adobe® Access™ per l&#39;utilizzo, copiare i file dal DVD. Questi file includono file JAR contenenti codice, certificati e classi di terze parti. Inoltre, richiedi un certificato da Adobe Systems Incorporated. Verranno rilasciate più credenziali utilizzate per proteggere l&#39;integrità del contenuto, delle licenze e della comunicazione in pacchetto tra client e server.

L’SDK per Adobe Access è disponibile in due tipi:
* SDK per Adobe Access Core
* SDK per Adobe Access Professional

La tabella seguente mostra un confronto di base tra gli SDK di Adobe Access:

| Funzione | SDK per Adobe Access Core | SDK per Adobe Access Professional |
|---|---|---|
| Funzioni di Flash Access 2.0 | Disponibile | Disponibile |
| Rotazione chiave | - | Disponibile |
| Supporto del dominio | Disponibile | Disponibile |
| Concatena delle licenze migliorata | Disponibile | Disponibile |
| Messaggi di sincronizzazione | Disponibile | Disponibile |
| Pre-generazione licenza | Disponibile | Disponibile |
| Licenze incorporate | Disponibile | Disponibile |

## Configurazione dell&#39;ambiente di sviluppo {#setting-up-the-development-environment}

Dal DVD, copia i seguenti file SDK da utilizzare nel tuo ambiente di sviluppo e nel tuo percorso di classe Java:

* adobe-flashaccess-certs.jar (contiene certificati radice di Adobe)
* adobe-flashaccess-sdk.jar (contiene le classi SDK di Adobe Access Core)
* adobe-flashaccess-sdk-pro.jar (contiene le classi Adobe Access Professional SDK, richieste solo per le funzioni Professional)

Sono necessari i seguenti file JAR di terze parti anche che si trovano sul DVD nella cartella &quot;third-party&quot; dell&#39;SDK:

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

Per migliorare le prestazioni, puoi facoltativamente abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche della piattaforma che si trovano nella cartella &quot;thirdparty/cryptoj&quot; dell’SDK. Per abilitare il supporto nativo, aggiungi la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux) al percorso. Vengono fornite le versioni a 32 bit e a 64 bit di queste librerie. La versione a 64 bit deve essere utilizzata solo se si dispone di un sistema operativo a 64 bit e si esegue la versione a 64 bit di Java.

Inoltre, una parte facoltativa dell&#39;SDK è adobe-flashaccess-lcrm.jar. Questo file è necessario solo per le funzionalità relative alla compatibilità di Adobe Flash Media Rights Management Server (FMRMS) 1.x. Se in precedenza è stato implementato FMRMS 1.x e non si desidera creare un pacchetto per i contenuti protetti da FMRMS, è necessario aggiungere il supporto al server licenze in modo che sia in grado di gestire contenuti e client obsoleti.
