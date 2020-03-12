---
seo-title: File delle proprietà del server
title: File delle proprietà del server
uuid: 3d3a0ee3-009f-4d62-9587-7e487ecdcafd
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# File delle proprietà del server {#server-properties-files}

Il server richiede due file di configurazione, uno per il server licenze e uno per il packager. Entrambi i file devono essere inseriti nel percorso di classe. I file delle proprietà contengono il percorso delle credenziali emesse da Adobe. Queste credenziali possono essere specificate come file .pfx e password oppure fornendo un alias e una password per una credenziale memorizzata in un HSM.

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

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Nell&#39;esempio precedente viene utilizzato il punto e virgola (;) come delimitatore. Per piattaforme diverse da Microsoft Windows, utilizzate due punti (:) come delimitatore.

L&#39;utilità genera la password crittografata, che è necessario copiare nel [!DNL .properties] file.
