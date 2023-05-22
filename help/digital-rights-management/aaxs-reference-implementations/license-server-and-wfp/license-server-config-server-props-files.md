---
title: File delle proprietà del server
description: File delle proprietà del server
copied-description: true
exl-id: c42fde8f-e438-4497-bd15-ebd0f6e2eed7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# File delle proprietà del server {#server-properties-files}

Il server richiede due file di configurazione, uno per il server licenze e uno per il packager. Entrambi i file devono essere posizionati nel percorso di classe. I file delle proprietà contengono la posizione delle credenziali emesse da Adobe. Queste credenziali possono essere specificate come file con estensione pfx e password oppure fornendo un alias e una password per una credenziale archiviata in un HSM.

Per informazioni dettagliate sui valori specifici e sull’utilizzo di ciascun parametro, consulta i file delle proprietà. I file delle proprietà di esempio si trovano nella directory &quot;resources&quot; dell&#39;implementazione di riferimento (Reference Implementation\Server\resources).

Per garantire la protezione della password delle credenziali, viene fornito uno strumento (ScrambleUtil.class) per crittografare la password prima che venga immessa nel file flashaccess-refimpl.properties o flashaccess-refimpl-packager.properties.

Per preparare correttamente la password delle credenziali:

1. Vai a [!DNL Reference Implementation\Server\refimpl\scrambler].
1. Dal prompt dei comandi immettere il comando:

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
>Nell&#39;esempio precedente viene utilizzato un punto e virgola (;) come delimitatore. Per le piattaforme diverse da Microsoft Windows, utilizza i due punti (:) come delimitatore.

L&#39;utility restituisce la password crittografata, che è necessario copiare in [!DNL .properties] file.
