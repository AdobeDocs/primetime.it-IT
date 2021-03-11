---
title: Determinare se il server licenze di implementazione di riferimento viene eseguito correttamente
description: Determinare se il server licenze di implementazione di riferimento viene eseguito correttamente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Determinare se il server delle licenze di implementazione di riferimento viene eseguito correttamente {#determining-if-reference-implementation-license-server-runs-properly}

Esistono diversi modi per determinare se il server delle licenze di implementazione di riferimento è stato avviato correttamente. È possibile visualizzare i registri [!DNL catalina.log] che potrebbero non essere sufficienti, in quanto il server di licenze accede ai propri file di registro. Segui i passaggi riportati di seguito per assicurarti che l’implementazione di riferimento sia stata avviata correttamente.

* Controlla il tuo file [!DNL AdobeFlashAccess.log]. In questo caso le informazioni di registro vengono scritte dall’implementazione di riferimento. La posizione di questo file di registro è indicata dal file [!DNL log4j.xml] e può essere modificata in modo da puntare a qualsiasi posizione desiderata. Per impostazione predefinita, il file di registro copiato nella directory di lavoro in cui viene eseguita la catalina.

* Vai al seguente URL: [!DNL https:// flashaccess/license/v4]*server:porta server*. Dovresti visualizzare il testo &quot;License Server è configurato correttamente&quot;.

Un altro modo per verificare se il server viene eseguito correttamente è quello di creare un pacchetto di un segmento del contenuto di test, impostare un lettore video di esempio e quindi riprodurlo.

La procedura seguente descrive questo processo:

1. Vai alla cartella [!DNL \Reference Implementation\Command Line Tools] .

   Consultare [Installazione degli strumenti della riga di comando](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) su come installare gli strumenti della riga di comando.

1. Digita il seguente comando per creare un semplice criterio DRM anonimo:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Consulta [Uso della riga di comando](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) su come creare criteri DRM con Gestione criteri DRM.

1. Imposta la proprietà `encrypt.license.serverurl` nel file [!DNL flashaccesstools.properties] sull&#39;URL del server licenze.

   Ad esempio, [!DNL https:// localhost:8080/]. Il file [!DNL flashaccesstools.properties] si trova nella cartella [!DNL \Reference Implementation\Command Line Tools] .

1. Digita il seguente comando per creare un pacchetto per un segmento del contenuto:

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

1. Copia i due file generati nella cartella [!DNL webapps\ROOT\Content] sul server Tomcat.
1. Vai alla directory [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] e copia il contenuto nella cartella [!DNL webapps\ROOT\SVP\] sul server Tomcat.

1. Installa Flash Player versione 10.1 o successiva.
1. Apri un browser web e vai al seguente URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Vai al seguente URL e fai clic su **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Se il video non viene riprodotto correttamente, controlla se nel riquadro di registrazione di Sample Video Player sono visualizzati dei codici di errore o li aggiunge al file [!DNL AdobeFlashAccess.log].

   Ora puoi cercare la posizione del file di registro [!DNL AdobeFlashAccess.log] nel file log4j.xml e quindi modificarlo. Per impostazione predefinita, il file di registro viene copiato nella directory di lavoro in cui viene eseguita la catalina.

