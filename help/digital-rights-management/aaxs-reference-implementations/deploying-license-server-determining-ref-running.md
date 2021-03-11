---
title: Determinare se il server licenze di implementazione di riferimento è in esecuzione correttamente
description: Determinare se il server licenze di implementazione di riferimento è in esecuzione correttamente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Determinare se il server delle licenze di implementazione di riferimento viene eseguito correttamente {#determining-if-reference-implementation-license-server-is-running-properly}

Esistono diversi modi per determinare se il server è stato avviato correttamente. La visualizzazione dei registri [!DNL catalina.log] potrebbe non essere sufficiente, in quanto il server licenze accede ai propri file di registro. Segui i passaggi riportati di seguito per assicurarti che l’implementazione di riferimento sia stata avviata correttamente.

* Controlla il tuo file [!DNL AdobeFlashAccess.log]. In questo caso le informazioni di registro vengono scritte dall’implementazione di riferimento. La posizione di questo file di registro è indicata dal file [!DNL log4j.xml] e può essere modificata in modo da puntare a qualsiasi posizione desiderata. Per impostazione predefinita, il file di registro viene inviato alla directory di lavoro in cui è stata eseguita la catalina.

* Passa al seguente URL: `https:///flashaccess/license/v4<your server:server port>`. Dovresti visualizzare il testo &quot;License Server è configurato correttamente&quot;.

Un altro modo per verificare se il server funziona correttamente è quello di creare un pacchetto di contenuti di prova, impostare un lettore video di esempio e riprodurlo. La procedura seguente descrive questo processo:

1. Passa alla cartella [!DNL \Reference Implementation\Command Line Tools] . Per informazioni sull&#39;installazione degli strumenti della riga di comando, vedere [Installazione degli strumenti della riga di comando](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Crea un semplice criterio anonimo utilizzando il seguente comando:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Per ulteriori informazioni sulla creazione di criteri tramite Gestione criteri, vedere [Uso della riga di comando](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Imposta la proprietà `encrypt.license.serverurl` nel file [!DNL flashaccesstools.properties] sull&#39;URL del server licenze (ad esempio, `https:// localhost:8080/`). Il file [!DNL flashaccesstools.properties] si trova sotto la cartella [!DNL \Reference Implementation\Command Line Tools] .

1. Crea un pacchetto di contenuti utilizzando il seguente comando:

   ```java
       java -jar libs\AdobePackager.jar  
   <i class="+ topic ph hi-d="" i "="">
   test_input_FLV  
   <i class="+ topic ph hi-d="" i "="">
   output_file  
               -p policy_test.pol 
   </i class="+ topic> 
   </i class="+ topic>
   ```

1. Copia i 2 file generati nella cartella Tomcat [!DNL webapps\ROOT\Content] .
1. Passa a `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` e copia il contenuto nella cartella Tomcat `webapps\ROOT\SVP\` .
1. Installa Flash Player 10.1 o versione successiva.
1. Apri il browser web e passa al seguente URL:

   `https:// localhost:8080/SVP/player.html`
1. Passa al seguente URL, quindi fai clic sul pulsante Play :

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Se la riproduzione del video non riesce, controlla se sono stati scritti codici di errore nel riquadro di registrazione del sample video player o nel file `AdobeFlashAccess.log`. La posizione del file di registro `AdobeFlashAccess.log` è indicata dal file log4j.xml e può essere modificata in modo che punti a qualsiasi posizione desideri. Per impostazione predefinita, il file di registro viene scritto nella directory di lavoro in cui è stata eseguita la catalina.
