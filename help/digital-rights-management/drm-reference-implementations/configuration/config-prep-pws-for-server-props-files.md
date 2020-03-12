---
description: 'null'
seo-description: 'null'
seo-title: Preparare le password per i file delle proprietà del server
title: Preparare le password per i file delle proprietà del server
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Preparare le password per i file delle proprietà del server{#prepare-passwords-for-the-server-properties-files}

L&#39;implementazione di riferimento fornisce `ScrambleUtil.class`, una classe che garantisce la sicurezza della password delle credenziali.

Utilizzare questo strumento per cifrare la password prima di includerla nel [!DNL flashaccess-refimpl.properties] file.

Per eseguire lo strumento, è possibile utilizzare uno script Ant o Java.

L&#39;utilità genera la password crittografata, che è necessario copiare nel [!DNL flashaccess-refimpl.properties] file.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Le password che sono state codificate con l&#39;implementazione di riferimento `ScrambleUtil.class` fornita non funzionano con il server DRM Primetime per lo streaming protetto.
