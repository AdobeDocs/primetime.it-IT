---
title: Creare criteri DRM personalizzati (facoltativo)
description: Creare criteri DRM personalizzati (facoltativo)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Creare criteri DRM personalizzati (facoltativo){#create-custom-drm-policies-optional}

Il kit di protezione DRM per Primetime Cloud viene fornito con alcuni criteri preconfigurati che possono essere utilizzati durante la creazione dei pacchetti. Se si desiderano configurazioni di criteri aggiuntive, ad esempio un diritto specifico per l’inserimento nell’elenco Consentiti da SWF, è possibile utilizzare Gestione criteri DRM Primetime incluso per generare criteri personalizzati.

>[!NOTE]
>
>Tutti i criteri devono utilizzare l’autenticazione ANONIMA (non Password nome utente o Personalizzata), indipendentemente dal fatto che venga utilizzato o meno il flusso di lavoro Autenticazione/Autorizzazione personalizzata.

Con Policy Manager è incluso [!DNL flashaccesstools.properties] file di configurazione, che è stato modificato per esporre solo le opzioni di policy configurabili supportate dal servizio DRM di Primetime Cloud. Se si impostano opzioni dei criteri non supportate dal servizio DRM di Primetime Cloud, si verificheranno errori di acquisizione della licenza. Per informazioni sull&#39;utilizzo di Primetime DRM Policy Manager, vedere: [Implementazioni di riferimento di Primetime DRM: Policy Manager](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Per creare un nuovo criterio, aggiorna il [!DNL flashaccesstools.properties] file come desiderato, quindi utilizzare il comando:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Creazione dinamica di criteri per autenticazione/adesione personalizzata{#create-policies-dynamically-for-custom-auth-entitlement}

Se si utilizza l&#39;autenticazione/titolazione personalizzata DRM di Primetime Cloud e si desidera creare in modo dinamico un nuovo criterio DRM per ogni richiesta di licenza (anziché richiamare i criteri da un pool pregenerato), l&#39;Adobe consiglia di utilizzare direttamente l&#39;SDK Java DRM di Primetime. L’utilizzo diretto dell’SDK Java è più veloce della [!DNL AdobePolicyManager.jar] che invia automaticamente il file della policy su disco, causando sovraccarico di I/O del disco.

Il codice di esempio che utilizza l’SDK Java è disponibile nella sezione [!DNL /Primetime DRM PolicyManager/sampleCode/] directory, denominata [!DNL CreatePolicy.java] e [!DNL CreatePolicyWithOutputProtection.java]. JavaScript e la documentazione per l’SDK Java sono disponibili all’indirizzo [Panoramica dell’SDK Adobe Primetime DRM](../../../digital-rights-management/drm-sdk-overview/overview.md)

Per generare ed eseguire gli esempi, copia i file .java nella cartella ../libs/ ed esegui:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
