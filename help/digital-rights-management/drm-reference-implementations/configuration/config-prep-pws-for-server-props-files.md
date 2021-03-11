---
title: Preparare le password per i file delle proprietà del server
description: Preparare le password per i file delle proprietà del server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---


# Prepara le password per i file delle proprietà del server{#prepare-passwords-for-the-server-properties-files}

L&#39;implementazione di riferimento fornisce `ScrambleUtil.class`, una classe che assicura la sicurezza della password delle credenziali.

Usa questo strumento per crittografare la password prima di includerla nel file [!DNL flashaccess-refimpl.properties].

Per eseguire lo strumento, è possibile utilizzare uno script Ant o Java.

L&#39;utility genera la password crittografata, che è necessario copiare nel file [!DNL flashaccess-refimpl.properties].

>[!NOTE]
>
>Le password codificate con `ScrambleUtil.class` fornite con l&#39;implementazione di riferimento non funzionano con il server DRM di Primetime per lo streaming protetto.
