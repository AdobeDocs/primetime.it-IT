---
title: Creare criteri DRM personalizzati (facoltativo)
description: Creare criteri DRM personalizzati (facoltativo)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Crea criteri DRM personalizzati (facoltativo){#create-custom-drm-policies-optional}

Il kit di protezione DRM di Primetime Cloud include alcuni criteri preconfigurati che possono essere utilizzati durante il packaging. Se desideri configurazioni di criteri aggiuntive, ad esempio un diritto di elenco Consentiti da SWF specifico, è possibile utilizzare Gestione criteri DRM di Primetime incluso per generare criteri personalizzati.

>[!NOTE]
>
>Tutti i criteri devono utilizzare l’autenticazione ANONYMOUS (non Password nome utente o Personalizzato), indipendentemente dal fatto che venga utilizzato o meno il flusso di lavoro di autenticazione/adesione personalizzata.

Incluso in Policy Manager è il file di configurazione [!DNL flashaccesstools.properties] che è stato modificato per esporre solo le opzioni di criteri configurabili supportate da Primetime Cloud DRM Service. L’impostazione delle opzioni dei criteri non supportate dal servizio DRM di Primetime Cloud genererà errori di acquisizione della licenza. Per informazioni sull&#39;utilizzo di Gestione criteri DRM di Primetime, fare riferimento a: [Implementazioni di riferimento DRM di Primetime: Policy Manager](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Per creare un nuovo criterio, aggiorna il file [!DNL flashaccesstools.properties] come desiderato, quindi utilizza il comando :

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Crea i criteri in modo dinamico per Autorizzazione personalizzata{#create-policies-dynamically-for-custom-auth-entitlement}

Se utilizzi l’autenticazione/autorizzazione personalizzata DRM di Primetime Cloud e desideri creare in modo dinamico un nuovo criterio DRM per ogni richiesta di licenza (invece di estrarre i criteri da un pool pregenerato), Adobe consiglia di utilizzare direttamente l’SDK Java DRM di Primetime. L&#39;utilizzo diretto dell&#39;SDK Java è più veloce dello strumento [!DNL AdobePolicyManager.jar] , che emette automaticamente il file dei criteri su disco, con conseguente sovraccarico di I/O del disco.

Il codice di esempio che utilizza l&#39;SDK Java si trova nella directory [!DNL /Primetime DRM PolicyManager/sampleCode/], denominata [!DNL CreatePolicy.java] e [!DNL CreatePolicyWithOutputProtection.java]. Javadocs e documentazione per l&#39;SDK Java sono disponibili in [Una panoramica dell&#39;SDK DRM di Adobe Primetime](../../../digital-rights-management/drm-sdk-overview/overview.md)

Per generare ed eseguire i campioni, copia i file .java nella cartella ../libs/ ed esegui:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
