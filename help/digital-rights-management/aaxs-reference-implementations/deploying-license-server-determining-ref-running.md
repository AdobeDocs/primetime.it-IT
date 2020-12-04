---
description: 'null'
seo-description: 'null'
seo-title: Determinare se il server delle licenze di implementazione di riferimento è in esecuzione correttamente
title: Determinare se il server delle licenze di implementazione di riferimento è in esecuzione correttamente
uuid: 84d32c94-7594-464e-a883-5338b52de2bf
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Determinare se il server delle licenze di implementazione di riferimento viene eseguito correttamente {#determining-if-reference-implementation-license-server-is-running-properly}

Esistono diversi modi per determinare se il server è stato avviato correttamente. La visualizzazione dei registri [!DNL catalina.log] potrebbe non essere sufficiente, in quanto il server licenze accede ai propri file di registro. Segui i passaggi indicati di seguito per verificare che l’implementazione di riferimento sia stata avviata correttamente.

* Controllare il file [!DNL AdobeFlashAccess.log]. In questa area vengono scritte le informazioni di registro relative all’implementazione di riferimento. Il percorso di questo file di registro è indicato dal file [!DNL log4j.xml] e può essere modificato in modo da puntare a qualsiasi posizione desiderata. Per impostazione predefinita, il file di registro viene inviato alla directory di lavoro in cui è stato eseguito il catalogo.

* Andate al seguente URL: `https:///flashaccess/license/v4<your server:server port>`. Viene visualizzato il testo &quot;License Server è configurato correttamente&quot;.

Un altro modo per verificare se il server funziona correttamente consiste nel creare un pacchetto di contenuti di prova, impostare un lettore video di esempio e riprodurlo. La procedura seguente descrive questo processo:

1. Andate alla cartella [!DNL \Reference Implementation\Command Line Tools]. Per informazioni sull&#39;installazione degli strumenti della riga di comando, vedere [Installazione degli strumenti della riga di comando](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Create un semplice criterio anonimo utilizzando il comando seguente:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Per ulteriori informazioni sulla creazione di criteri tramite Gestione criteri, vedere [Uso della riga di comando](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Impostate la proprietà `encrypt.license.serverurl` nel file [!DNL flashaccesstools.properties] sull&#39;URL del server licenze (ad esempio, `https:// localhost:8080/`). Il file [!DNL flashaccesstools.properties] si trova nella cartella [!DNL \Reference Implementation\Command Line Tools].

1. Create un pacchetto di contenuti utilizzando il seguente comando:

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

1. Copiate i 2 file generati nella cartella Tomcat [!DNL webapps\ROOT\Content].
1. Andate a `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` e copiate il contenuto nella cartella Tomcat `webapps\ROOT\SVP\`.
1. Installare l&#39;Flash Player 10.1 o successivo.
1. Aprite il browser Web e passate al seguente URL:

   `https:// localhost:8080/SVP/player.html`
1. Andate al seguente URL, quindi fate clic sul pulsante Riproduci:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Se il video non viene riprodotto correttamente, verificate se nel riquadro di registrazione di Sample Video Player o nel file `AdobeFlashAccess.log` sono stati scritti dei codici di errore. Il percorso del file di registro `AdobeFlashAccess.log` è indicato dal file log4j.xml e può essere modificato in modo da puntare a qualsiasi posizione desiderata. Per impostazione predefinita, il file di registro viene scritto nella directory di lavoro in cui è stata eseguita la catalina.
