---
description: Per impostare l'Adobe ® Access™, copiare i file dal DVD. Questi file includono file JAR contenenti codice, certificati e classi di terze parti. Inoltre, richiedi un certificato a Adobe Systems Incorporated. Verranno rilasciate più credenziali utilizzate per proteggere l'integrità dei pacchetti di contenuto, licenze e comunicazioni tra client e server.
title: Configurazione dell’ambiente di sviluppo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Configurazione dell’SDK {#setting-up-the-sdk}

Per impostare l&#39;Adobe ® Access™, copiare i file dal DVD. Questi file includono file JAR contenenti codice, certificati e classi di terze parti. Inoltre, richiedi un certificato a Adobe Systems Incorporated. Verranno rilasciate più credenziali utilizzate per proteggere l&#39;integrità dei pacchetti di contenuto, licenze e comunicazioni tra client e server.

L’SDK di accesso di Adobe è disponibile in due tipi:
* SDK per Adobe Access Core
* SDK per Adobe Access Professional

Nella tabella seguente viene illustrato un confronto di base tra gli SDK di Adobe Access:

| Funzionalità | SDK per Adobe Access Core | SDK per Adobe Access Professional |
|---|---|---|
| Caratteristiche di Flash Access 2.0 | Disponibile | Disponibile |
| Rotazione chiave | - | Disponibile |
| Supporto dominio | Disponibile | Disponibile |
| Concatenamento licenze migliorato | Disponibile | Disponibile |
| Messaggi di sincronizzazione | Disponibile | Disponibile |
| Licenza di pre-generazione | Disponibile | Disponibile |
| Licenze integrate | Disponibile | Disponibile |

## Configurazione dell’ambiente di sviluppo {#setting-up-the-development-environment}

Dal DVD, copia i seguenti file SDK da utilizzare nell’ambiente di sviluppo e nel percorso di classe Java:

* adobe-flashaccess-certs.jar (contiene Adobi di certificati radice)
* adobe-flashaccess-sdk.jar (contiene le classi SDK di Adobe Access Core)
* adobe-flashaccess-sdk-pro.jar (contiene le classi SDK di Adobe Access Professional, necessarie solo per le funzioni professionali)

Nella cartella &quot;third party&quot; dell&#39;SDK, è necessario che anche i seguenti file JAR di terze parti si trovino sul DVD:

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

Per migliorare le prestazioni, puoi facoltativamente abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche per la piattaforma che si trovano nella cartella &quot;third party/cryptoj&quot; dell’SDK. Per abilitare il supporto nativo, aggiungi la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux) al percorso. Vengono fornite le versioni a 32 bit e a 64 bit di queste librerie. Si noti che la versione a 64 bit deve essere utilizzata solo se si dispone di un sistema operativo a 64 bit e si esegue la versione a 64 bit di Java.

Inoltre, una parte opzionale dell&#39;SDK è adobe-flashaccess-lcrm.jar. Questo file è necessario solo per funzionalità relative alla compatibilità Adobe Flash Media Rights Management Server (FMRMS) 1.x. Se in precedenza è stato distribuito FMRMS 1.x e non si desidera creare un nuovo pacchetto del contenuto protetto da FMRMS, è necessario aggiungere il supporto al server licenze in modo che sia in grado di gestire i vecchi contenuti e client.
