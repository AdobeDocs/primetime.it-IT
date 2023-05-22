---
title: Determinare se Reference Implementation License Server è in esecuzione correttamente
description: Determinare se Reference Implementation License Server è in esecuzione correttamente
copied-description: true
exl-id: ef28e169-f8d2-4c7f-b606-aa4e811aae9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Determinare se Reference Implementation License Server è in esecuzione correttamente {#determining-if-reference-implementation-license-server-is-running-properly}

Esistono diversi modi per determinare se il server è stato avviato correttamente. Visualizzazione di [!DNL catalina.log] i registri potrebbero non essere sufficienti, in quanto il server licenze registra i propri file di registro. Segui i passaggi seguenti per assicurarti che l’implementazione di riferimento sia stata avviata correttamente.

* Controlla il tuo [!DNL AdobeFlashAccess.log] file. In questo punto l’implementazione di riferimento scrive le informazioni di registro. La posizione di questo file di registro è indicata dal [!DNL log4j.xml] e possono essere modificati in modo da puntare a una posizione desiderata. Per impostazione predefinita, il file di registro viene inviato alla directory di lavoro in cui è stato eseguito catalina.

* Passa all’URL seguente: `https:///flashaccess/license/v4<your server:server port>`. Dovresti trovare il testo &quot;License Server is setup correct&quot; (Il server licenze è configurato correttamente).

Un altro modo per verificare se il server funziona correttamente consiste nel creare un pacchetto del contenuto di prova, impostare un lettore video di esempio e riprodurlo. La procedura seguente descrive questo processo:

1. Accedi a [!DNL \Reference Implementation\Command Line Tools] cartella. Per informazioni sull&#39;installazione degli strumenti della riga di comando, vedere [Installazione degli strumenti della riga di comando](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Crea un criterio anonimo semplice utilizzando il comando seguente:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Per ulteriori informazioni sulla creazione di criteri tramite Gestione criteri, vedere [Utilizzo della riga di comando](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Imposta il `encrypt.license.serverurl` proprietà in [!DNL flashaccesstools.properties] all&#39;URL del server licenze (ad esempio, `https:// localhost:8080/`). Il [!DNL flashaccesstools.properties] il file si trova sotto [!DNL \Reference Implementation\Command Line Tools] cartella.

1. Creare un pacchetto di contenuto utilizzando il comando seguente:

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

1. Copia i 2 file generati nel Tomcat [!DNL webapps\ROOT\Content] cartella.
1. Accedi a `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` e copia il contenuto nel Tomcat `webapps\ROOT\SVP\` cartella.
1. Installa Flash Player 10.1 o versione successiva.
1. Apri il browser web e passa al seguente URL:

   `https:// localhost:8080/SVP/player.html`
1. Passa all’URL seguente, quindi fai clic sul pulsante Riproduci:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Se il video non viene riprodotto correttamente, verificare se sono stati scritti codici di errore nel riquadro di registrazione del lettore video di esempio o nel `AdobeFlashAccess.log` file. La posizione del `AdobeFlashAccess.log` Il file di registro è indicato dal file log4j.xml e può essere modificato in modo da puntare a una posizione desiderata. Per impostazione predefinita, il file di registro viene scritto nella directory di lavoro in cui è stato eseguito catalina.
