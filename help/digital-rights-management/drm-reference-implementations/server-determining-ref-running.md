---
title: Determinare se il server licenze di implementazione di riferimento funziona correttamente
description: Determinare se il server licenze di implementazione di riferimento funziona correttamente
copied-description: true
exl-id: 97ca0b6c-2661-4cdc-b8d0-dcc545f009f6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Determinare se il server licenze di implementazione di riferimento funziona correttamente {#determining-if-reference-implementation-license-server-runs-properly}

Esistono diversi modi per determinare se il server licenze di implementazione di riferimento è stato avviato correttamente. È possibile visualizzare [!DNL catalina.log] i registri potrebbero non essere sufficienti, in quanto il server licenze registra i propri file di registro. Segui i passaggi seguenti per assicurarti che l’implementazione di riferimento sia stata avviata correttamente.

* Controlla il tuo [!DNL AdobeFlashAccess.log] file. In questo punto l’implementazione di riferimento scrive le informazioni di registro. La posizione di questo file di registro è indicata dal [!DNL log4j.xml] e possono essere modificati in modo da puntare a una posizione desiderata. Per impostazione predefinita, il file di log viene copiato nella directory di lavoro in cui viene eseguito catalina.

* Vai al seguente URL: [!DNL https:// flashaccess/license/v4]*server:porta server*. Dovresti trovare il testo &quot;License Server is setup correct&quot; (Il server licenze è configurato correttamente).

Un altro modo per verificare se il server funziona correttamente consiste nel creare un pacchetto di un segmento del contenuto di test, impostare un lettore video di esempio e quindi riprodurlo.

La procedura seguente descrive questo processo:

1. Vai a [!DNL \Reference Implementation\Command Line Tools] cartella.

   Consulta [Installazione degli strumenti della riga di comando](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) su come installare gli strumenti della riga di comando.

1. Digitare il comando seguente per creare un semplice criterio DRM anonimo:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Consulta [Utilizzo della riga di comando](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) su come creare criteri DRM con DRM Policy Manager.

1. Imposta il `encrypt.license.serverurl` proprietà in [!DNL flashaccesstools.properties] all&#39;URL del server licenze.

   Ad esempio: [!DNL https:// localhost:8080/]. Il [!DNL flashaccesstools.properties] il file si trova in [!DNL \Reference Implementation\Command Line Tools] cartella.

1. Digita il seguente comando per creare un pacchetto di un segmento del contenuto:

```
       java -jar libs\AdobePackager.jar  
       <i class="+ topic ph hi-d="" i "="">
         test_input_FLV  
        <i class="+ topic ph hi-d="" i "="">
       output_file  
               -p policy_test.pol 
       </i class="+ topic> 
       </i class="+ topic>
```

1. Copia i due file generati in [!DNL webapps\ROOT\Content] sul server Tomcat.
1. Vai a [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] e copiare il contenuto nella directory [!DNL webapps\ROOT\SVP\] sul server Tomcat.

1. Installare Flash Player versione 10.1 o successiva.
1. Apri un browser web e passa al seguente URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Vai all’URL seguente e fai clic su **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Se il video non viene riprodotto correttamente, verificare se nel riquadro di registrazione del lettore video di esempio sono visualizzati codici di errore o se questi sono stati aggiunti al [!DNL AdobeFlashAccess.log] file.

   Ora puoi cercare il percorso del [!DNL AdobeFlashAccess.log] nel file log4j.xml, quindi modificarlo. Per impostazione predefinita, il file di registro viene copiato nella directory di lavoro in cui viene eseguito catalina.
