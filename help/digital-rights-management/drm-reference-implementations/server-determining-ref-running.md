---
description: 'null'
seo-description: 'null'
seo-title: Determinare se il server delle licenze di implementazione di riferimento viene eseguito correttamente
title: Determinare se il server delle licenze di implementazione di riferimento viene eseguito correttamente
uuid: afd82d6d-a11c-48ff-b48c-8f81d4b406a0
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Determinare se il server delle licenze di implementazione di riferimento viene eseguito correttamente {#determining-if-reference-implementation-license-server-runs-properly}

Esistono diversi modi per determinare se il server delle licenze di implementazione di riferimento è stato avviato correttamente. È possibile visualizzare i registri [!DNL catalina.log] che potrebbero non essere sufficienti, poiché il server licenze accede ai propri file di registro. Segui i passaggi indicati di seguito per verificare che l’implementazione di riferimento sia stata avviata correttamente.

* Controllare il file [!DNL AdobeFlashAccess.log]. In questa area vengono scritte le informazioni di registro relative all’implementazione di riferimento. Il percorso di questo file di registro è indicato dal file [!DNL log4j.xml] e può essere modificato in modo da puntare a qualsiasi posizione desiderata. Per impostazione predefinita, il file di registro copiato nella directory di lavoro in cui si esegue catalina.

* Andate al seguente URL: [!DNL https:// flashaccess/license/v4]*server:porta server*. Viene visualizzato il testo &quot;License Server è configurato correttamente&quot;.

Un altro modo per verificare se il server viene eseguito correttamente consiste nel creare un pacchetto per un segmento del contenuto di prova, impostare un lettore video di esempio e riprodurlo.

La procedura seguente descrive questo processo:

1. Andate alla cartella [!DNL \Reference Implementation\Command Line Tools].

   Per informazioni sull&#39;installazione degli strumenti della riga di comando, vedere [Installazione degli strumenti della riga di comando](../drm-reference-implementations/command-line-tools/install-command-line-tools.md).

1. Digitate il comando seguente per creare un semplice criterio DRM anonimo:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Vedere [Uso della riga di comando](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) su come creare criteri DRM con Gestione criteri DRM.

1. Impostate la proprietà `encrypt.license.serverurl` nel file [!DNL flashaccesstools.properties] sull&#39;URL del server licenze.

   Ad esempio, [!DNL https:// localhost:8080/]. Il file [!DNL flashaccesstools.properties] si trova nella cartella [!DNL \Reference Implementation\Command Line Tools].

1. Digitate il comando seguente per creare un pacchetto per un segmento del contenuto:

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

1. Copiate i due file generati nella cartella [!DNL webapps\ROOT\Content] del server Tomcat.
1. Andate alla directory [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] e copiate il contenuto nella cartella [!DNL webapps\ROOT\SVP\] sul server Tomcat.

1. Installate la versione di Flash Player 10.1 o successiva.
1. Aprite un browser Web e passate al seguente URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Accedete al seguente URL e fate clic su **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Se il video non viene riprodotto correttamente, verificate che nel riquadro di registrazione di Sample Video Player siano visualizzati eventuali codici di errore o aggiunti al file [!DNL AdobeFlashAccess.log].

   Ora è possibile cercare il percorso del file di registro [!DNL AdobeFlashAccess.log] nel file log4j.xml e quindi modificarlo. Per impostazione predefinita, il file di registro viene copiato nella directory di lavoro in cui si esegue catalina.

