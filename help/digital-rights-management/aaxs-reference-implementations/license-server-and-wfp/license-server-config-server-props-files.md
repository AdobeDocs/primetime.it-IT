---
seo-title: File delle proprietà del server
title: File delle proprietà del server
uuid: 3d3a0ee3-009f-4d62-9587-7e487ecdcafd
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# File delle proprietà del server {#server-properties-files}

Il server richiede due file di configurazione, uno per il server licenze e uno per il packager. Entrambi i file devono essere inseriti nel percorso di classe. I file delle proprietà contengono il percorso delle credenziali emesse dal Adobe . Queste credenziali possono essere specificate come file .pfx e password oppure fornendo un alias e una password per una credenziale memorizzata in un HSM.

Fare riferimento ai file delle proprietà per informazioni dettagliate sui valori specifici e sull&#39;utilizzo di ciascun parametro. I file delle proprietà di esempio si trovano nella directory &quot;resources&quot; dell&#39;implementazione di riferimento (Riferimento Implementation\Server\resources).

Per garantire la sicurezza della password della credenziale, viene fornito uno strumento (ScrambleUtil.class) per crittografare la password prima che venga inserita nel file flashaccess-refimpl.properties o flashaccess-refimpl-packager.properties.

Per preparare correttamente la password della credenziale:

1. Vai a [!DNL Reference Implementation\Server\refimpl\scrambler].
1. Dal prompt dei comandi, immettere il comando:

   ```
   java -classpath  
   <i class="+ topic ph hi-d="" i "="">
   path_to_adobe-flashaccess-sdk.jar.; 
        com.adobe.flashaccess.refimpl.util.ScrambleUtil " 
   <i class="+ topic ph hi-d="" i "="">
   your_pfx_password" 
   </i class="+ topic> 
   </i class="+ topic>
   ```

>[!NOTE]
>
>Nell&#39;esempio precedente viene utilizzato il punto e virgola (;) come delimitatore. Per piattaforme diverse da Microsoft Windows, utilizzate due punti (:) come delimitatore.

L&#39;utilità genera la password crittografata, che è necessario copiare nel [!DNL .properties] file.
