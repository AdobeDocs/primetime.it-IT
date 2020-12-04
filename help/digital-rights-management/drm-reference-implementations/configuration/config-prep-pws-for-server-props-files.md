---
description: 'null'
seo-description: 'null'
seo-title: Preparare le password per i file delle proprietà del server
title: Preparare le password per i file delle proprietà del server
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Preparare le password per i file delle proprietà del server{#prepare-passwords-for-the-server-properties-files}

L&#39;implementazione del riferimento fornisce `ScrambleUtil.class`, una classe che garantisce la sicurezza della password delle credenziali.

Utilizzare questo strumento per cifrare la password prima di includerla nel file [!DNL flashaccess-refimpl.properties].

Per eseguire lo strumento, è possibile utilizzare uno script Ant o Java.

L&#39;utilità genera la password crittografata, che è necessario copiare nel file [!DNL flashaccess-refimpl.properties].

>[!NOTE]
>
>Le password codificate con il `ScrambleUtil.class` fornito con l&#39;implementazione di riferimento non funzionano con il server DRM di Primetime per lo streaming protetto.
